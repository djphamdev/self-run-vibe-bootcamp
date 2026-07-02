---
layout: default
title: "Module 5: Hermes Agent"
description: "Master the Hermes Agent runtime. Skills, plugins, cron, sub-agents, memory, multi-channel. The OpenClaw replacement."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 5 · ~4 hrs · The agentic runtime</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">
      Hermes <span class="accent">Agent</span>
    </h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      Self-hosted, multi-model, multi-channel. Skills, plugins, cron, sub-agents, memory.
      This replaces OpenClaw — production-ready, fully yours.
    </p>
  </div>
</div>

<div class="container" style="max-width: 900px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">🎯</span>
    <p><strong>Goal:</strong> A running Hermes gateway with: 3 custom skills, 2 cron jobs, Discord + CLI channels, persistent memory. You can chat with it, schedule it, and it remembers.</p>
  </div>

  <h2>🏗 Architecture mental model</h2>
  <div class="grid grid-3">
    <div class="card">
      <div class="icon">🧠</div>
      <h3>Core</h3>
      <p>Single Python process. Loads config, discovers skills, starts gateway, manages channels.</p>
    </div>
    <div class="card">
      <div class="icon">🧩</div>
      <h3>Skills</h3>
      <p>Python functions + docstrings. Auto-discovered. LLM decides when to call.</p>
    </div>
    <div class="card">
      <div class="icon">🔌</div>
      <h3>Plugins</h3>
      <p>Structured extensions. Config, multiple tools, persistent state.</p>
    </div>
    <div class="card">
      <div class="icon">⏰</div>
      <h3>Cron</h3>
      <p>YAML/JSON schedule. Per-job model, delivery target, retries, silent marker.</p>
    </div>
    <div class="card">
      <div class="icon">👥</div>
      <h3>Sub-agents</h3>
      <p>Spawn specialized agents. Tree of execution. Share memory.</p>
    </div>
    <div class="card">
      <div class="icon">💾</div>
      <h3>Memory</h3>
      <p>SQLite + vector store. Persists across sessions. Vector search built-in.</p>
    </div>
    <div class="card">
      <div class="icon">📡</div>
      <h3>Channels</h3>
      <p>CLI, Discord, Telegram, webhook. Same agent, multiple interfaces.</p>
    </div>
  </div>

  <h2>🚀 Quick start (15 min)</h2>

  <h3>1. Install</h3>
  <div class="prompt">git clone https://github.com/DonZzzilla/hermesDonZzz.git ~/projects/hermes
cd ~/projects/hermes
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
hermes init</div>

  <h3>2. Configure (~/.hermes/config.yaml)</h3>
  <details class="code-block">
    <summary>config.yaml</summary>
    <pre><code>provider: openrouter
openrouter:
  api_key: "${OPENROUTER_API_KEY}"
  base_url: "https://openrouter.ai/api/v1"
  default_model: "qwen/qwen-2.5-coder-32b-instruct:free"
  fallback_model: "google/gemini-2.0-flash-exp:free"

channels:
  cli: { enabled: true }
  discord:
    enabled: true
    bot_token: "${DISCORD_BOT_TOKEN}"
    allowed_guilds: ["1333668222892769341"]
    default_channel: "1516475197027389521"

memory:
  backend: sqlite
  path: "~/.hermes/memory/state.db"
  vector:
    backend: chromadb
    path: "~/.hermes/memory/vectors"

cron:
  enabled: true
  jobs_file: "~/.hermes/cron/jobs.json"
</code></pre>
  </details>

  <h3>3. Run</h3>
  <div class="prompt">hermes gateway start    # daemon: runs cron, listens on channels
hermes chat "hi"        # CLI test
hermes chat --channel discord "status?"  # Discord test</div>

  <h2>🛠 Build 3 skills (exercise)</h2>
  <p>Create <code>~/.hermes/skills/</code> and add these. Hermes auto-discovers on gateway restart.</p>

  <h3>Skill 1: Web Search</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/web_search.py</summary>
    <pre><code>"""Search the web via DuckDuckGo HTML. Returns top results with snippets."""
import requests
from bs4 import BeautifulSoup

def web_search(query: str, max_results: int = 5) -> list[dict]:
    """Search the web. Args: query (str), max_results (int, default 5). Returns list of {title, url, snippet}."""
    url = "https://html.duckduckgo.com/html/"
    params = {"q": query}
    headers = {"User-Agent": "Mozilla/5.0"}
    resp = requests.post(url, data=params, headers=headers, timeout=10)
    soup = BeautifulSoup(resp.text, "html.parser")
    results = []
    for result in soup.select(".result__snippet")[:max_results]:
        title_elem = result.find_previous("a", class_="result__snippet")
        link_elem = result.find_previous("a", class_="result__url")
        results.append({
            "title": title_elem.get_text(strip=True) if title_elem else "",
            "url": link_elem.get("href", "") if link_elem else "",
            "snippet": result.get_text(strip=True)[:300]
        })
    return results
</code></pre>
  </details>

  <h3>Skill 2: Memory Save/Recall</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/memory_tool.py</summary>
    <pre><code>"""Save and recall facts from persistent memory with tags."""
from hermes.memory import Memory

def remember(key: str, value: str, tags: list[str] = []) -> str:
    """Save a fact with optional tags. Example: remember('user_prefers_dark', 'true', ['prefs'])"""
    mem = Memory()
    mem.store(key, value, tags=tags)
    return f"Remembered: {key} = {value} (tags: {tags})"

def recall(key: str) -> str:
    """Retrieve a fact by exact key."""
    mem = Memory()
    return mem.get(key) or f"No memory for '{key}'"

def recall_by_tag(tag: str) -> list[dict]:
    """Retrieve all facts with a tag. Great for project context."""
    mem = Memory()
    return mem.search_by_tag(tag)
</code></pre>
  </details>

  <h3>Skill 3: Discord Send</h3>
  <details class="code-block">
    <summary>~/.hermes/skills/discord_send.py</summary>
    <pre><code>"""Send messages to Discord via webhook."""
import requests, os

WEBHOOK_URL = os.getenv("DISCORD_WEBHOOK_URL")

def discord_send(content: str, username: str = "Hermes", embed: dict = None) -> bool:
    """Send to Discord channel. If webhook not set, prints to console."""
    if not WEBHOOK_URL:
        print(f"[DISCORD] {content}")
        return False
    payload = {"content": content, "username": username}
    if embed:
        payload["embeds"] = [embed]
    r = requests.post(WEBHOOK_URL, json=payload, timeout=5)
    return r.status_code == 204

def discord_embed(title: str, description: str, url: str = None, color: int = 0x5865F2) -> dict:
    """Build a Discord embed object."""
    e = {"title": title, "description": description, "color": color}
    if url:
        e["url"] = url
    return e
</code></pre>
  </details>

  <h2>⏰ Cron jobs (exercise: 2 jobs)</h2>
  <p>Edit <code>~/.hermes/cron/jobs.json</code>:</p>
  <details class="code-block">
    <summary>jobs.json</summary>
    <pre><code>{
  "jobs": [
    {
      "id": "morning-briefing",
      "schedule": "0 9 * * *",
      "prompt": "Search web for 'AI agents 2026'. Get top 3 articles. Summarize each in 2 sentences. Send to Discord with embed: title, summary, link. Tag memory with 'briefing:2026-$(date +%F)'.",
      "model": "google/gemini-2.0-flash-exp:free",
      "delivery": "discord:1516475197027389521",
      "silent_marker": "[SILENT]"
    },
    {
      "id": "flight-tracker",
      "schedule": "0 */6 * * *",
      "prompt": "Check flight prices for LAX→NRT on 2026-12-20 (non-stop only). If any fare drops below $800, alert via Discord with booking link. If no change, output [SILENT].",
      "model": "qwen/qwen-2.5-coder-32b-instruct:free",
      "delivery": "discord:1516475197027389521",
      "silent_marker": "[SILENT]"
    }
  ]
}
</code></pre>
  </details>

  <h3>Test manually (don't wait for schedule)</h3>
  <div class="prompt">hermes cron run morning-briefing
hermes cron run flight-tracker
hermes cron list</div>

  <h2>💬 Multi-channel: Discord setup</h2>
  <ol>
    <li>Create Discord app → Bot → copy token</li>
    <li>Enable: Message Content Intent, Server Members Intent</li>
    <li>OAuth2 → Bot → permissions: Send Messages, Embed Links, Read Messages</li>
    <li>Invite to your server</li>
    <li>Right-click channel → Copy Channel ID</li>
    <li>Right-click server → Copy Server ID</li>
    <li>Add to <code>config.yaml</code> and <code>.env</code></li>
  </ol>

  <h2>✅ Done criteria</h2>
  <ul>
    <li>☐ <code>hermes gateway start</code> runs without errors</li>
    <li>☐ <code>hermes chat "search for AI agents"</code> calls web_search skill</li>
    <li>☐ <code>hermes chat "remember my favorite color is purple"</code> saves to memory</li>
    <li>☐ <code>hermes chat "what's my favorite color?"</code> recalls from memory</li>
    <li>☐ <code>hermes cron run morning-briefing</code> posts to Discord</li>
    <li>☐ <code>hermes chat --channel discord "ping"</code> replies in Discord</li>
    <li>☐ Gateway runs overnight — cron fires at 9am, you get briefing</li>
  </ul>

  <h2>🎯 The two commands you'll live in</h2>
  <div class="grid grid-2">
    <div class="card" style="border-color: var(--accent);">
      <h3 style="color: var(--accent-2);">/goal "your objective"</h3>
      <p>Tell Hermes what you want. It plans, breaks it down, executes autonomously.</p>
      <div class="prompt">/goal "build a flight tracker that checks prices daily and alerts me when my LAX→JFK trip drops under $300"</div>
    </div>
    <div class="card" style="border-color: var(--success);">
      <h3 style="color: var(--success);">/yolo</h3>
      <p>Full autonomous mode. No confirmations. Write code, run tests, deploy, iterate.</p>
      <div class="prompt">/yolo "deploy the flight tracker to GitHub Pages with a custom domain"</div>
    </div>
  </div>

  <div class="callout">
    <span class="icon-c">💡</span>
    <p><strong>Workflow:</strong> Use free AI (OpenRouter web, Claude Code free, ChatGPT) to <em>design/validate</em> first. Then hand to Hermes with <code>/goal</code> or <code>/yolo</code> to execute. Free AI for thinking, Hermes for doing.</p>
  </div>

  <h2>💰 Build for Money, Not Just Skills</h2>
  <div class="callout" style="border-color: var(--warning); background: rgba(210, 153, 34, 0.1);">
    <span class="icon-c">🎯</span>
    <p><strong>Critical reminder:</strong> Vibe coding builds skills, but <em>shipping to paying customers</em> builds a business.</p>
    <p>Before you write code: <strong>find a real problem</strong> → talk to 5 people who'd pay → ask "would you pay $X/mo?" → ship smallest paid thing → iterate with real users (strangers with credit cards).</p>
    <p>Don't vibe code for an audience of you. Skills without revenue = hobby. We're aiming for money.</p>
  </div>

  <h2>📚 Resources</h2>
  <ul>
    <li><a href="https://hermes-agent.nousresearch.com/docs" target="_blank">Official Hermes docs</a></li>
    <li><a href="https://github.com/DonZzzilla/hermesDonZzz" target="_blank">Our fork</a> (backup scripts, custom skills)</li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p6">Starter Kit P6: HN Daily Digest</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p7">Starter Kit P7: Content Pipeline</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p8">Starter Kit P8: Flight Tracker</a></li>
    <li><a href="{{ '/syllabus/' | relative_url }}#module-6">Next: Module 6 — Multi-Agent Workflows</a></li>
  </ul>

  <div class="hero-actions" style="margin-top: 40px;">
    <a href="{{ '/starter-kits/' | relative_url }}" class="btn btn-primary">⚡ Copy a Hermes starter kit</a>
    <a href="{{ '/syllabus/' | relative_url }}" class="btn btn-ghost">← Back to syllabus</a>
  </div>

</div>