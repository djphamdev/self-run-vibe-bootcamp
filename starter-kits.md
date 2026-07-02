---
layout: default
title: "Starter Kits"
description: "Copy-pasteable project templates for the Self-Run Vibe Bootcamp. Each kit is a working v0 you can ship in one session."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 7 · Copy-paste → ship → iterate</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">
      Starter <span class="accent">Kits</span>
    </h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      Each kit is a complete v0: code you can copy, run, and deploy in 30 minutes.
      No setup paralysis. Ship something real, then improve it.
    </p>
  </div>
</div>

<div class="container" style="max-width: 1000px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">⚡</span>
    <p>
      <strong>How to use:</strong> Click a kit → copy the files into a new repo →
      <code>npm install && npm run dev</code> (or <code>python -m http.server</code> for static)
      → push to GitHub → enable Pages → done. Then iterate with Hermes.
    </p>
  </div>

  <h2>🌱 Beginner Kits (static, no backend)</h2>

  <div class="grid grid-2">
    <div class="card">
      <div class="mono accent">// KIT-P1</div>
      <h3>Blog + Semantic Search</h3>
      <p>Jekyll blog with ChromaDB embeddings. Search by meaning, not keywords.</p>
      <div class="tags">
        <span class="tag">Jekyll</span>
        <span class="tag">ChromaDB</span>
        <span class="tag">Python</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>blog-search/
├── _posts/              # Your markdown posts
├── embed.py             # Embed posts → ChromaDB
├── search.html          # Search UI (vanilla JS)
├── search.js            # Query Chroma, render results
├── requirements.txt     # chromadb, sentence-transformers
└── Gemfile              # Jekyll</code></pre>
      </details>
      <div class="prompt">
# embed.py — run once after writing posts
import chromadb
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')
client = chromadb.PersistentClient(path="./chroma")
col = client.get_or_create_collection("posts")

for post in Path("_posts").glob("*.md"):
    text = post.read_text()
    # split into chunks, embed, upsert
    chunks = chunk_text(text, 500)
    embeddings = model.encode(chunks).tolist()
    col.add(documents=chunks, embeddings=embeddings, ids=[f"{post.stem}-{i}" for i in range(len(chunks))])
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>

    <div class="card">
      <div class="mono accent">// KIT-P2</div>
      <h3>Daily Quote + LLM Reflection</h3>
      <p>GitHub Action runs daily → fetches quote → asks LLM for reflection → commits new page.</p>
      <div class="tags">
        <span class="tag">GitHub Actions</span>
        <span class="tag">OpenRouter</span>
        <span class="tag">Jekyll</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>daily-reflection/
├── .github/workflows/daily.yml
├── _reflections/        # Auto-generated daily pages
├── fetch_quote.py       # Get quote + call LLM
├── _layouts/reflection.html
└── index.html           # Lists all reflections</code></pre>
      </details>
      <div class="prompt">
# .github/workflows/daily.yml
name: Daily Reflection
on:
  schedule:
    - cron: '0 6 * * *'  # 6am UTC
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
      - run: pip install openai
      - env:
          OPENROUTER_API_KEY: ${{ secrets.OPENROUTER_API_KEY }}
        run: python fetch_quote.py
      - run: |
          git config user.name "bot"
          git config user.email "bot@users.noreply.github.com"
          git add _reflections/
          git commit -m "Daily reflection $(date +%F)" || exit 0
          git push
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>

    <div class="card">
      <div class="mono accent">// KIT-P4</div>
      <h3>RSS → Podcast (TTS)</h3>
      <p>Cron fetches RSS → LLM summarizes → TTS to MP3 → static podcast feed.</p>
      <div class="tags">
        <span class="tag">Python</span>
        <span class="tag">TTS</span>
        <span class="tag">RSS</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>rss-to-podcast/
├── fetch_and_speak.py
├── episodes/            # MP3s + JSON metadata
├── feed.xml             # iTunes-compatible RSS
├── requirements.txt     # feedparser, openai, edge-tts
└── .github/workflows/daily.yml</code></pre>
      </details>
      <div class="prompt">
# fetch_and_speak.py
import feedparser, asyncio, edge_tts, openai

client = openai.OpenAI(base_url="https://openrouter.ai/api/v1", api_key=os.getenv("OPENROUTER_API_KEY"))

feed = feedparser.parse("https://example.com/rss.xml")
for entry in feed.entries[:3]:  # top 3
    # Summarize
    resp = client.chat.completions.create(
        model="google/gemini-2.0-flash-exp:free",
        messages=[{"role": "user", "content": f"Summarize in 2 sentences for audio: {entry.summary}"}]
    )
    summary = resp.choices[0].message.content
    # TTS
    communicate = edge_tts.Communicate(summary, "en-US-AriaNeural")
    await communicate.save(f"episodes/{entry.id}.mp3")
    # Append to feed.xml...
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>

    <div class="card">
      <div class="mono accent">// KIT-P8</div>
      <h3>Flight Price Tracker (Hermes)</h3>
      <p>Hermes cron checks specific dates (non-stop only) → alerts via Discord/Telegram when price drops.</p>
      <div class="tags">
        <span class="tag">Hermes</span>
        <span class="tag">Cron</span>
        <span class="tag">Discord</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>flight-tracker/
├── ~/.hermes/cron/jobs.json
├── skills/flight_search.py
├── skills/price_check.py
└── skills/discord_alert.py</code></pre>
      </details>
      <div class="prompt">
# ~/.hermes/cron/jobs.json
{
  "jobs": [
    {
      "id": "flight-tracker-lax-nrt",
      "schedule": "0 */6 * * *",  # every 6 hours
      "prompt": "Check flight prices for LAX→NRT on 2026-12-20 (non-stop only). If any fare drops below $800, alert via Discord with booking link.",
      "model": "qwen/qwen-2.5-coder-32b-instruct:free",
      "delivery": "discord:123456789012345678",
      "silent_marker": "[SILENT]"
    }
  ]
}
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>
  </div>

  <h2>🌿 Intermediate Kits (backend required)</h2>

  <div class="grid grid-2">
    <div class="card">
      <div class="mono accent">// KIT-P5</div>
      <h3>Ask-My-Repo (RAG)</h3>
      <p>Convex backend + GitHub Pages front-end. Index any repo, ask questions grounded in actual code.</p>
      <div class="tags">
        <span class="tag">Convex</span>
        <span class="tag">RAG</span>
        <span class="tag">TypeScript</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>ask-my-repo/
├── convex/
│   ├── schema.ts
│   ├── embeddings.ts      # OpenRouter embeddings
│   ├── ingest.ts          # GitHub API → chunk → embed
│   └── search.ts          # Vector search + LLM answer
├── frontend/
│   ├── index.html
│   ├── search.js
│   └── styles.css
└── package.json</code></pre>
      </details>
      <div class="prompt">
# convex/ingest.ts — GitHub → Convex vectors
import { internal } from "./_generated/api";
import { httpAction } from "convex/server";

export const ingestRepo = httpAction(async (ctx, { owner, repo }) => {
  const files = await fetchGitHubTree(owner, repo);
  for (const file of files) {
    if (isCodeFile(file.path)) {
      const content = await fetchGitHubFile(owner, repo, file.path);
      const chunks = chunkCode(content, 500);
      const embeddings = await embedTexts(chunks);
      for (let i = 0; i < chunks.length; i++) {
        await ctx.db.insert("chunks", {
          repo: `${owner}/${repo}`,
          path: file.path,
          chunkIndex: i,
          text: chunks[i],
          embedding: embeddings[i],
        });
      }
    }
  }
});
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>

    <div class="card">
      <div class="mono accent">// KIT-P6</div>
      <h3>Hacker News Daily Digest</h3>
      <p>Hermes cron scrapes HN → LLM scores by your interests → Discord at 8am with top 5.</p>
      <div class="tags">
        <span class="tag">Hermes</span>
        <span class="tag">Cron</span>
        <span class="tag">Discord</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>hn-digest/
├── ~/.hermes/cron/jobs.json
├── skills/hn_scrape.py
├── skills/hn_score.py
└── skills/discord_digest.py</code></pre>
      </details>
      <div class="prompt">
# ~/.hermes/cron/jobs.json
{
  "jobs": [
    {
      "id": "hn-digest",
      "schedule": "0 8 * * *",  # 8am daily
      "prompt": "Fetch top 50 Hacker News stories. Score each 1-10 for relevance to: AI agents, local-first software, dev tools, Rust. Pick top 5. Format as Discord embed with title, score, reason, link. Send to Discord.",
      "model": "google/gemini-2.0-flash-exp:free",
      "delivery": "discord:123456789012345678"
    }
  ]
}
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>

    <div class="card">
      <div class="mono accent">// KIT-P7</div>
      <h3>Multi-Agent Content Pipeline</h3>
      <p>4 Hermes agents (researcher→writer→critic→publisher) coordinated via cron + shared memory.</p>
      <div class="tags">
        <span class="tag">Hermes</span>
        <span class="tag">Multi-agent</span>
        <span class="tag">Memory</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>content-pipeline/
├── ~/.hermes/cron/jobs.json
├── skills/researcher.py
├── skills/writer.py
├── skills/critic.py
└── skills/publisher.py</code></pre>
      </details>
      <div class="prompt">
# ~/.hermes/cron/jobs.json — 4 agents, staggered
{
  "jobs": [
    { "id": "researcher", "schedule": "0 9 * * *", "prompt": "Research 'local-first AI tools 2026'. Find 10 sources. Save titles+URLs+key points to memory with tag 'research:local-ai-2026'.", "model": "qwen/qwen-2.5-coder-32b-instruct:free" },
    { "id": "writer", "schedule": "0 11 * * *", "prompt": "Read memory tag 'research:local-ai-2026'. Write a 1500-word blog post for developers. Save draft to memory with tag 'draft:local-ai-2026'.", "model": "google/gemini-2.0-flash-exp:free" },
    { "id": "critic", "schedule": "0 13 * * *", "prompt": "Read memory tag 'draft:local-ai-2026'. Critique: clarity, accuracy, tone, missing topics. Save improved version to 'final:local-ai-2026'.", "model": "qwen/qwen-2.5-coder-32b-instruct:free" },
    { "id": "publisher", "schedule": "0 15 * * *", "prompt": "Read 'final:local-ai-2026'. Commit as _posts/$(date +%F)-local-ai-2026.md to GitHub Pages repo. Push. Notify Discord.", "model": "google/gemini-2.0-flash-exp:free", "delivery": "discord:123456789012345678" }
  ]
}
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>

    <div class="card">
      <div class="mono accent">// KIT-P12</div>
      <h3>LLM Eval Harness (Live Leaderboard)</h3>
      <p>Compare 5+ free models on same prompts. Side-by-side UI. Public leaderboard on GitHub Pages.</p>
      <div class="tags">
        <span class="tag">OpenRouter</span>
        <span class="tag">Eval</span>
        <span class="tag">Vanilla JS</span>
      </div>
      <details class="code-block">
        <summary>📁 Show file structure</summary>
        <pre><code>eval-harness/
├── run_eval.py            # Runs prompts across models
├── results/               # JSON results per run
├── index.html             # Side-by-side comparison UI
├── leaderboard.js         # Renders results table
└── prompts.yaml           # Test cases</code></pre>
      </details>
      <div class="prompt">
# run_eval.py
import openai, yaml, json, os

client = openai.OpenAI(base_url="https://openrouter.ai/api/v1", api_key=os.getenv("OPENROUTER_API_KEY"))
MODELS = [
    "qwen/qwen-2.5-coder-32b-instruct:free",
    "google/gemini-2.0-flash-exp:free",
    "meta-llama/llama-3.1-8b-instruct:free",
    "mistralai/mistral-nemo:free",
]
PROMPTS = yaml.safe_load(open("prompts.yaml"))

results = {}
for model in MODELS:
    results[model] = {}
    for name, prompt in PROMPTS.items():
        resp = client.chat.completions.create(model=model, messages=[{"role": "user", "content": prompt}])
        results[model][name] = resp.choices[0].message.content

# Save timestamped results
ts = datetime.now().isoformat()
Path(f"results/{ts}.json").write_text(json.dumps(results, indent=2))
      </div>
      <a href="#" class="more">📋 Copy starter →</a>
    </div>
  </div>

  <h2>🔧 Hermes Skills Library (drop-in)</h2>
  <p>Copy any skill into <code>~/.hermes/skills/</code> — Hermes auto-discovers on restart.</p>

  <div class="grid grid-2">
    <div class="card">
      <h3>🔍 Web Search Skill</h3>
      <div class="prompt">
# ~/.hermes/skills/web_search.py
"""Search the web and return top results with snippets."""
import requests, os

def web_search(query: str, max_results: int = 5) -> list[dict]:
    """Search DuckDuckGo HTML (no API key needed). Returns [{title, url, snippet}, ...]."""
    url = "https://html.duckduckgo.com/html/"
    params = {"q": query}
    headers = {"User-Agent": "Mozilla/5.0"}
    resp = requests.post(url, data=params, headers=headers)
    from bs4 import BeautifulSoup
    soup = BeautifulSoup(resp.text, "html.parser")
    results = []
    for r in soup.select(".result__snippet")[:max_results]:
        link = r.find_previous("a", class_="result__url")
        title = r.find_previous("a", class_="result__snippet")
        results.append({
            "title": title.get_text(strip=True) if title else "",
            "url": link.get("href", "") if link else "",
            "snippet": r.get_text(strip=True)[:300]
        })
    return results
      </div>
    </div>

    <div class="card">
      <h3>💾 Memory Save/Recall Skill</h3>
      <div class="prompt">
# ~/.hermes/skills/memory_tool.py
"""Save and recall facts from persistent memory."""
from hermes.memory import Memory

def remember(key: str, value: str, tags: list[str] = []) -> str:
    """Save a fact. Example: remember('user_prefers_dark', 'true', ['prefs'])"""
    mem = Memory()
    mem.store(key, value, tags=tags)
    return f"Remembered: {key} = {value}"

def recall(key: str) -> str:
    """Retrieve a fact by exact key."""
    mem = Memory()
    return mem.get(key) or f"No memory for '{key}'"

def recall_by_tag(tag: str) -> list[dict]:
    """Retrieve all facts with a tag. Great for project context."""
    mem = Memory()
    return mem.search_by_tag(tag)
      </div>
    </div>

    <div class="card">
      <h3>📁 File Ops Skill</h3>
      <div class="prompt">
# ~/.hermes/skills/file_ops.py
"""Read, write, list files in a sandboxed workspace."""
import os
from pathlib import Path

WORKSPACE = Path(os.getenv("HERMES_WORKSPACE", "~/hermes_workspace")).expanduser()
WORKSPACE.mkdir(exist_ok=True)

def read_file(path: str) -> str:
    """Read a file from the workspace."""
    return (WORKSPACE / path).read_text()

def write_file(path: str, content: str) -> str:
    """Write a file to the workspace."""
    (WORKSPACE / path).write_text(content)
    return f"Wrote {path}"

def list_files(pattern: str = "*") -> list[str]:
    """List files matching pattern."""
    return [str(f.relative_to(WORKSPACE)) for f in WORKSPACE.glob(pattern)]

def run_python(path: str) -> str:
    """Execute a Python file in the workspace and return stdout."""
    import subprocess
    result = subprocess.run(["python3", str(WORKSPACE / path)], capture_output=True, text=True, timeout=30)
    return result.stdout + result.stderr
      </div>
    </div>

    <div class="card">
      <h3>💬 Discord Send Skill</h3>
      <div class="prompt">
# ~/.hermes/skills/discord_send.py
"""Send a message to a Discord channel via webhook."""
import requests, os

WEBHOOK_URL = os.getenv("DISCORD_WEBHOOK_URL")

def discord_send(content: str, username: str = "Hermes", embed: dict = None) -> bool:
    """Send to Discord. If webhook not set, prints to console."""
    if not WEBHOOK_URL:
        print(f"[DISCORD] {content}")
        return False
    payload = {"content": content, "username": username}
    if embed:
        payload["embeds"] = [embed]
    r = requests.post(WEBHOOK_URL, json=payload)
    return r.status_code == 204

def discord_embed(title: str, description: str, url: str = None, color: int = 0x5865F2) -> dict:
    """Build a Discord embed object."""
    return {"title": title, "description": description, "url": url, "color": color}
      </div>
    </div>
  </div>

  <h2>🎓 How to level up a kit</h2>
  <ol>
    <li><strong>Ship the v0</strong> — copy kit, deploy, get a live URL</li>
    <li><strong>Add one feature</strong> — use Hermes <code>/goal</code> to add it</li>
    <li><strong>Make it yours</strong> — customize UI, add your data, solve your problem</li>
    <li><strong>Validate</strong> — show 5 people, ask "would you pay $X/mo?"</li>
    <li><strong>Charge</strong> — Stripe link + manual process = revenue v1</li>
  </ol>

  <div class="callout">
    <span class="icon-c">💡</span>
    <p>
      <strong>Pro tip:</strong> Each kit has a matching Hermes cron job or skill.
      The static kits (P1-P4) are great for learning GitHub Pages + Actions.
      The Hermes kits (P5-P12) teach you the agentic runtime. Do both.
    </p>
  </div>

</div>