---
layout: default
title: "Module 6: Multi-Agent Workflows"
description: "Coordinate multiple Hermes agents via cron + shared memory. Build production pipelines: researcher → writer → critic → publisher."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 6 · ~3 hrs · Agent orchestration</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">
      Multi-Agent <span class="accent">Workflows</span>
    </h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      OpenClaw does peer-to-peer coordination (alpha). Hermes does cron + shared memory + skills (production).
      Same outcome, zero experimental risk.
    </p>
  </div>
</div>

<div class="container" style="max-width: 900px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">🎯</span>
    <p><strong>Goal:</strong> A 4-agent content pipeline that runs daily: Researcher → Writer → Critic → Publisher. Each reads/writes shared memory. You monitor from Discord.</p>
  </div>

  <h2>🧠 The coordination model</h2>
  <p>No peer-to-peer protocol. No service discovery. Just:</p>
  <ol>
    <li><strong>Cron</strong> — triggers each agent on a schedule</li>
    <li><strong>Shared memory</strong> — SQLite + vector store, tagged by stage</li>
    <li><strong>Skills</strong> — each agent has its own toolkit</li>
    <li><strong>Delivery</strong> — Discord/Telegram for monitoring</li>
  </ol>
  <p>This is how production systems work. Scheduled jobs. Shared database. Observability.</p>

  <h2>🏗 The 4-agent pipeline</h2>
  <table class="compare">
    <thead>
      <tr><th>Agent</th><th>Cron</th><th>Input (memory tag)</th><th>Output (memory tag)</th><th>Skills</th></tr>
    </thead>
    <tbody>
      <tr><td><strong>Researcher</strong></td><td>0 9 * * *</td><td>—</td><td><code>research:topic-YYYY-MM-DD</code></td><td>web_search, memory_tool</td></tr>
      <tr><td><strong>Writer</strong></td><td>0 11 * * *</td><td><code>research:...</code></td><td><code>draft:topic-YYYY-MM-DD</code></td><td>memory_tool, file_ops</td></tr>
      <tr><td><strong>Critic</strong></td><td>0 13 * * *</td><td><code>draft:...</code></td><td><code>final:topic-YYYY-MM-DD</code></td><td>memory_tool</td></tr>
      <tr><td><strong>Publisher</strong></td><td>0 15 * * *</td><td><code>final:...</code></td><td>GitHub Pages commit</td><td>file_ops, terminal, discord_send</td></tr>
    </tbody>
  </table>

  <h2>⚙️ Cron config (copy to ~/.hermes/cron/jobs.json)</h2>
  <details class="code-block">
    <summary>jobs.json — content pipeline</summary>
    <pre><code>{
  "jobs": [
    {
      "id": "researcher",
      "schedule": "0 9 * * *",
      "prompt": "Topic: 'local-first AI tools 2026'. Search web for 10 sources. For each: title, URL, 3 key points. Save to memory with tag 'research:local-ai-$(date +%F)'. Include source URLs for citation.",
      "model": "qwen/qwen-2.5-coder-32b-instruct:free",
      "delivery": "local"
    },
    {
      "id": "writer",
      "schedule": "0 11 * * *",
      "prompt": "Read memory tag 'research:local-ai-$(date +%F)'. Write a 1500-word technical blog post for developers. Structure: intro, 5 tools with pros/cons, comparison table, conclusion. Save draft to memory with tag 'draft:local-ai-$(date +%F)'.",
      "model": "google/gemini-2.0-flash-exp:free",
      "delivery": "local"
    },
    {
      "id": "critic",
      "schedule": "0 13 * * *",
      "prompt": "Read memory tag 'draft:local-ai-$(date +%F)'. Critique: 1) Technical accuracy 2) Clarity 3) Missing topics 4) Tone. Produce improved version. Save to 'final:local-ai-$(date +%F)'.",
      "model": "qwen/qwen-2.5-coder-32b-instruct:free",
      "delivery": "local"
    },
    {
      "id": "publisher",
      "schedule": "0 15 * * *",
      "prompt": "Read memory tag 'final:local-ai-$(date +%F)'. Create Jekyll post at _posts/$(date +%F)-local-ai-2026.md with front matter. Commit and push to GitHub Pages repo. Send Discord notification with link.",
      "model": "google/gemini-2.0-flash-exp:free",
      "delivery": "discord:1516475197027389521",
      "silent_marker": "[SILENT]"
    }
  ]
}
</code></pre>
  </details>

  <h3>Test each agent manually</h3>
  <div class="prompt">hermes cron run researcher
hermes cron run writer
hermes cron run critic
hermes cron run publisher</div>

  <h2>🛠 Skills each agent needs</h2>

  <h3>Researcher skills</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/researcher.py</summary>
    <pre><code>"""Researcher agent skills: web search + memory."""
from hermes.memory import Memory
import requests, os

def research_topic(topic: str, max_sources: int = 10) -> list[dict]:
    """Search web, extract key points, return structured sources."""
    # Use web_search skill (already loaded)
    results = web_search(topic, max_results=max_sources)
    sources = []
    for r in results:
        # Could fetch full page here for more detail
        sources.append({
            "title": r["title"],
            "url": r["url"],
            "summary": r["snippet"],
            "key_points": extract_key_points(r["snippet"])
        })
    return sources

def save_research(tag: str, sources: list[dict]) -> str:
    """Save research to memory with tag."""
    mem = Memory()
    content = "\n\n".join([f"## {s['title']}\nURL: {s['url']}\nKey points:\n" + "\n".join(f"- {p}" for p in s['key_points']) for s in sources])
    mem.store(tag, content, tags=["research", tag])
    return f"Saved {len(sources)} sources to {tag}"
</code></pre>
  </details>

  <h3>Writer skills</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/writer.py</summary>
    <pre><code>"""Writer agent skills: read research, write post."""
from hermes.memory import Memory

def write_post(research_tag: str, draft_tag: str, word_target: int = 1500) -> str:
    """Read research, write blog post, save draft."""
    mem = Memory()
    research = mem.get(research_tag)
    if not research:
        return f"No research found at {research_tag}"
    
    prompt = f"""Write a {word_target}-word technical blog post based on this research:
    
    {research}
    
    Structure:
    1. Hook intro (why this matters now)
    2. 5 tools with pros/cons
    3. Comparison table
    4. When to use each
    5. Conclusion + next steps
    
    Tone: Senior engineer writing for developers. Concrete, no fluff."""
    
    # LLM writes the post (handled by Hermes prompt)
    # We just save the output
    mem.store(draft_tag, "{{LLM_OUTPUT}}", tags=["draft", draft_tag])
    return f"Draft saved to {draft_tag}"
</code></pre>
  </details>

  <h3>Critic skills</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/critic.py</summary>
    <pre><code>"""Critic agent skills: review and improve."""
from hermes.memory import Memory

def critique_draft(draft_tag: str, final_tag: str) -> str:
    """Read draft, critique, save final."""
    mem = Memory()
    draft = mem.get(draft_tag)
    if not draft:
        return f"No draft found at {draft_tag}"
    
    prompt = f"""Review this draft. Output ONLY the improved version.
    
    Checklist:
    - Technical accuracy: any wrong claims?
    - Clarity: would a junior dev understand?
    - Completeness: missing obvious tools?
    - Tone: senior engineer, not marketing
    - Formatting: headers, code blocks, tables
    
    Draft:
    {draft}
    
    Output the full improved post."""
    
    mem.store(final_tag, "{{LLM_OUTPUT}}", tags=["final", final_tag])
    return f"Final version saved to {final_tag}"
</code></pre>
  </details>

  <h3>Publisher skills</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/publisher.py</summary>
    <pre><code>"""Publisher agent skills: commit to GitHub Pages, notify Discord."""
import subprocess, os
from hermes.memory import Memory

def publish_post(final_tag: str, repo_path: str = "~/projects/blog") -> str:
    """Read final, write Jekyll post, git commit, push."""
    mem = Memory()
    content = mem.get(final_tag)
    if not content:
        return f"No final content at {final_tag}"
    
    # Generate filename
    from datetime import date
    today = date.today().isoformat()
    slug = final_tag.replace("final:", "").replace(":", "-")
    filename = f"_posts/{today}-{slug}.md"
    
    # Front matter + content
    front_matter = f"""---
layout: post
title: "Local-First AI Tools 2026"
date: {today}
tags: [ai, local-first, tools]
---
"""
    full_content = front_matter + "\n" + content
    
    # Write file
    repo = os.path.expanduser(repo_path)
    filepath = os.path.join(repo, filename)
    os.makedirs(os.path.dirname(filepath), exist_ok=True)
    with open(filepath, "w") as f:
        f.write(full_content)
    
    # Git commit + push
    subprocess.run(["git", "add", filename], cwd=repo, check=True)
    subprocess.run(["git", "commit", "-m", f"Add post: {slug}"], cwd=repo, check=True)
    subprocess.run(["git", "push"], cwd=repo, check=True)
    
    return f"Published: https://yourname.github.io/{today}-{slug}/"

def discord_notify(url: str, title: str) -> bool:
    """Send Discord embed with post link."""
    import requests
    webhook = os.getenv("DISCORD_WEBHOOK_URL")
    if not webhook:
        return False
    embed = {"title": title, "url": url, "color": 0x3FB950, "description": "New post published via Hermes pipeline 🤖"}
    requests.post(webhook, json={"embeds": [embed]})
    return True
</code></pre>
  </details>

  <h2>🔁 Variations to try</h2>
  <div class="grid grid-2">
    <div class="card">
      <h3>Parallel research</h3>
      <p>Run 3 researchers at 9am on different topics. Writer at 11am merges all three.</p>
      <div class="prompt"># jobs.json
{ "id": "research-ai", "schedule": "0 9 * * *", ... },
{ "id": "research-rust", "schedule": "0 9 * * *", ... },
{ "id": "research-local", "schedule": "0 9 * * *", ... },
{ "id": "writer", "schedule": "0 11 * * *", "prompt": "Read research:ai, research:rust, research:local. Merge into one post." }
</div>
    </div>
    <div class="card">
      <h3>Human-in-the-loop</h3>
      <p>Critic posts to Discord for approval. Publisher only runs after 👍 reaction.</p>
      <div class="prompt"># critic delivery: discord
# publisher: triggered by Discord webhook on 👍 reaction
# (needs a small Discord bot to listen for reactions)
</div>
    </div>
    <div class="card">
      <h3>Code pipeline</h3>
      <p>Researcher finds APIs → Writer generates code → Critic runs tests → Publisher deploys.</p>
      <div class="prompt"># writer prompt: "Generate FastAPI endpoints for the APIs found"
# critic prompt: "Run pytest. Fix failures. Repeat until green."
# publisher: "Deploy to Fly.io / Railway / Render"
</div>
    </div>
    <div class="card">
      <h3>Distributed Hermes</h3>
      <p>Multiple Pis (yours, friend's, VPS) each run Hermes. Share findings via Convex/webhook.</p>
      <div class="prompt"># Each Hermes has same cron, different data sources
# Webhook skill posts to shared Convex backend
# Dashboard aggregates all findings
</div>
    </div>
  </div>

  <h2>✅ Done criteria</h2>
  <ul>
    <li>☐ All 4 cron jobs defined in <code>jobs.json</code></li>
    <li>☐ <code>hermes cron run researcher</code> saves to memory tag</li>
    <li>☐ <code>hermes cron run writer</code> reads research, saves draft</li>
    <li>☐ <code>hermes cron run critic</code> reads draft, saves final</li>
    <li>☐ <code>hermes cron run publisher</code> commits to GitHub, posts to Discord</li>
    <li>☐ Pipeline runs automatically overnight — you wake up to a published post</li>
    <li>☐ (Bonus) Add a 5th agent: <code>promoter</code> at 17:00 tweets the link</li>
  </ul>

  <h2>💰 Build for Money, Not Just Skills</h2>
  <div class="callout" style="border-color: var(--warning); background: rgba(210, 153, 34, 0.1);">
    <span class="icon-c">🎯</span>
    <p><strong>This pipeline IS a product.</strong> People pay for:</p>
    <ul>
      <li>Daily curated tech digests (email/Discord/Telegram)</li>
      <li>Weekly industry reports (sold via Stripe)</li>
      <li>Competitor monitoring for startups</li>
      <li>SEO content at scale</li>
    </ul>
    <p>Ship the pipeline → find 5 people who'd pay $29/mo → charge them. That's the bootcamp outcome.</p>
  </div>

  <h2>📚 Resources</h2>
  <ul>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p6">Starter Kit P6: HN Daily Digest</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p7">Starter Kit P7: Content Pipeline</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p11">Starter Kit P11: Decentralized Research Network</a></li>
    <li><a href="https://hermes-agent.nousresearch.com/docs" target="_blank">Hermes cron docs</a></li>
    <li><a href="{{ '/syllabus/' | relative_url }}#module-7">Next: Module 7 — Ship It</a></li>
  </ul>

  <div class="hero-actions" style="margin-top: 40px;">
    <a href="{{ '/starter-kits/' | relative_url }}" class="btn btn-primary">⚡ Copy the pipeline starter</a>
    <a href="{{ '/syllabus/' | relative_url }}" class="btn btn-ghost">← Back to syllabus</a>
  </div>

</div>