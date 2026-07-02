---
layout: default
title: "Hermes Agent"
description: "Hermes Agent is the open-source agentic runtime that replaces OpenClaw in our stack. Skills, plugins, cron, sub-agents, multi-channel."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 800px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 5 · The agentic runtime · Free · Self-hosted</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">
      Hermes <span class="accent">Agent</span>
    </h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      An open-source agentic runtime for vibe coding. Self-hosted, multi-model,
      multi-channel, with skills, plugins, cron jobs, and sub-agents. This is
      what we use instead of OpenClaw.
    </p>
  </div>
</div>

<div class="container" style="max-width: 900px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">🤖</span>
    <p>
      <strong>What it is:</strong> a single Python process you run on a Pi, a
      laptop, or a VPS. It can chat with you on Discord, Telegram, or CLI, run
      scheduled jobs, call any LLM via OpenRouter, and execute code in sandboxes.
      Think of it as a personal AI ops layer.
    </p>
  </div>

  <h2>🧠 Core concepts</h2>

  <div class="grid grid-3">
    <div class="card">
      <div class="icon">🧩</div>
      <h3>Skills</h3>
      <p>Modular capabilities. Web search, file ops, code execution, vector recall.
      Drop in your own. Hermes auto-discovers them.</p>
    </div>
    <div class="card">
      <div class="icon">🔌</div>
      <h3>Plugins</h3>
      <p>Extend the runtime. Convex backend, GitHub API, Discord webhooks.
      Build a plugin, register it, done.</p>
    </div>
    <div class="card">
      <div class="icon">⏰</div>
      <h3>Cron jobs</h3>
      <p>Schedule anything. "Wake up at 9am, fetch X, summarize, post to Discord."
      YAML config, isolated runs, full logs.</p>
    </div>
    <div class="card">
      <div class="icon">👥</div>
      <h3>Sub-agents</h3>
      <p>Spawn specialized agents for sub-tasks. A researcher that calls a writer
      that calls a critic. Tree of execution.</p>
    </div>
    <div class="card">
      <div class="icon">💾</div>
      <h3>Memory</h3>
      <p>Persistent state across sessions. SQLite + vector store. The agent
      remembers yesterday's context.</p>
    </div>
    <div class="card">
      <div class="icon">📡</div>
      <h3>Multi-channel</h3>
      <p>Discord, Telegram, CLI, webhook. Same agent, many interfaces.
      One conversation thread across all.</p>
    </div>
  </div>

  <h2>🚀 Quick start</h2>
  <h3>1. Install</h3>
  <div class="prompt">git clone https://github.com/DonZzzilla/hermesDonZzz.git ~/projects/hermes
cd ~/projects/hermes
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
hermes init</div>

  <h3>2. Configure OpenRouter</h3>
  <div class="prompt">cat > ~/.hermes/config.yaml <<'EOF'
provider: openrouter
openrouter:
  api_key: "${OPENROUTER_API_KEY}"
  base_url: "https://openrouter.ai/api/v1"
  default_model: "qwen/qwen-2.5-coder-32b-instruct:free"
  fallback_model: "google/gemini-2.0-flash-exp:free"

channels:
  cli: { enabled: true }
  discord: { enabled: false }

memory:
  backend: sqlite
  path: "~/.hermes/memory/state.db"
  vector:
    backend: chromadb
    path: "~/.hermes/memory/vectors"

cron:
  enabled: true
  jobs_file: "~/.hermes/cron/jobs.json"
EOF</div>

  <h3>3. Run it</h3>
  <div class="prompt">hermes gateway start  # starts the daemon
hermes chat "what's 2+2?"  # CLI test
# or
hermes chat --channel discord  # talk via Discord</div>

  <h2 id="multi-agent">👥 Multi-agent workflows</h2>

  <p>The killer feature: <strong>Hermes is the OpenClaw replacement</strong>.
  Where OpenClaw does peer-to-peer agent coordination, Hermes does it via
  cron + shared memory + skills. Same outcome, production-ready, fully under
  your control.</p>

  <h3>Example: a 4-agent content pipeline</h3>
  <div class="prompt"># ~/.hermes/cron/jobs.json
{
  "jobs": [
    {
      "id": "researcher",
      "schedule": "0 9 * * *",
      "agent": "researcher",
      "prompt": "Find 5 articles on AI dev. Save to memory."
    },
    {
      "id": "writer",
      "schedule": "0 11 * * *",
      "agent": "writer",
      "prompt": "Read researcher's finds. Write 1 blog post."
    },
    {
      "id": "critic",
      "schedule": "0 13 * * *",
      "agent": "critic",
      "prompt": "Review the writer's draft. Suggest 3 improvements."
    },
    {
      "id": "publisher",
      "schedule": "0 15 * * *",
      "agent": "publisher",
      "prompt": "Take final draft. Push to GitHub Pages repo."
    }
  ]
}</div>

  <p>Each agent reads from shared memory, writes to shared memory, and you can
  watch the whole pipeline from a single Discord channel.</p>

  <h2>🛠 Building skills</h2>
  <p>A skill is just a Python file with a docstring and a function. Hermes reads
  the docstring and exposes it to the LLM.</p>

  <div class="prompt"># ~/.hermes/skills/weather.py
"""
Get current weather for a city.
Args: city (str) - city name
Returns: dict with temp, condition, humidity
"""
import requests

def get_weather(city: str) -> dict:
    r = requests.get(f"https://wttr.in/{city}?format=j1")
    data = r.json()
    current = data["current_condition"][0]
    return {
        "temp_c": current["temp_C"],
        "condition": current["weatherDesc"][0]["value"],
        "humidity": current["humidity"]
    }</div>

  <p>That's it. Hermes auto-discovers it. Ask "what's the weather in Tokyo?" and
  the LLM will call your skill.</p>

  <h2>📋 Useful built-in skills</h2>
  <ul>
    <li><strong>web_search</strong> — search the web, return top results</li>
    <li><strong>web_extract</strong> — fetch and parse a URL</li>
    <li><strong>read_file / write_file / patch</strong> — file operations</li>
    <li><strong>terminal</strong> — run shell commands</li>
    <li><strong>search_files</strong> — find files by name or content</li>
    <li><strong>execute_code</strong> — run Python with full tool access</li>
    <li><strong>discord_admin</strong> — manage Discord servers</li>
    <li><strong>process</strong> — manage background processes</li>
  </ul>

  <h2>🪝 Plugins: extend with anything</h2>
  <p>Plugins are more structured than skills. They can hold config, multiple
  tools, persistent state.</p>

  <h3>Example: Convex plugin</h3>
  <div class="prompt"># ~/.hermes/plugins/convex/plugin.py
from hermes_plugins import Plugin, tool

class ConvexPlugin(Plugin):
    name = "convex"

    def setup(self):
        self.deploy_url = self.config["deploy_url"]
        self.admin_key = self.config["admin_key"]

    @tool
    def convex_query(self, function: str, args: dict = None) -> dict:
        """Run a Convex query."""
        ...

    @tool
    def convex_mutation(self, function: str, args: dict = None) -> dict:
        """Run a Convex mutation."""
        ...</div>

  <h2>💬 Multi-channel examples</h2>

  <h3>Discord</h3>
  <div class="prompt"># ~/.hermes/config.yaml
channels:
  discord:
    enabled: true
    bot_token: "${DISCORD_BOT_TOKEN}"
    allowed_guilds: ["1333668222892769341"]
    default_channel: "1516475197027389521"</div>
  <p>Now your agent is a Discord bot. Same skills, same memory, Discord UI.</p>

  <h3>Telegram</h3>
  <div class="prompt">channels:
  telegram:
    enabled: true
    bot_token: "${TELEGRAM_BOT_TOKEN}"
    allowed_chats: ["8815461875"]</div>

  <h3>CLI</h3>
  <div class="prompt">hermes chat --session dev "explain this code" < src/foo.py</div>

  <h2>⏰ Cron deep-dive</h2>
  <p>Hermes cron is YAML or JSON, with per-job model override, retries, and
  delivery targets.</p>

  <table class="compare">
    <thead>
      <tr><th>Field</th><th>Description</th></tr>
    </thead>
    <tbody>
      <tr><td><code>id</code></td><td>unique identifier</td></tr>
      <tr><td><code>schedule</code></td><td>cron expression (5-field)</td></tr>
      <tr><td><code>prompt</code></td><td>what the agent should do</td></tr>
      <tr><td><code>model</code></td><td>override default model</td></tr>
      <tr><td><code>delivery</code></td><td>"origin" / "local" / "discord:CHANNEL_ID"</td></tr>
      <tr><td><code>silent_marker</code></td><td>use "[SILENT]" to suppress output on no-op</td></tr>
      <tr><td><code>retry</code></td><td>max attempts, backoff</td></tr>
    </tbody>
  </table>

  <h2>💡 Patterns we love</h2>

  <h3>1. The "morning briefing"</h3>
  <p>9am cron → fetch weather, news, calendar → summarize → push to Discord.
  Replaces a $20/mo personal AI service.</p>

  <h3>2. The "always-on monitor"</h3>
  <p>15-min cron → check price of X → if threshold met, alert via TTS.
  The 5800X3D stock tracker lives here.</p>

  <h3>3. The "research assistant"</h3>
  <p>Topic → agent searches → summarizes → saves to vector memory →
  follow-up agent can query that memory later. The RAG loop is implicit.</p>

  <h3>4. The "deploy bot"</h3>
  <p>Trigger on git push → run tests → if green, deploy to GitHub Pages →
  notify Discord. CI/CD as a cron job.</p>

  <h2>🔒 Security notes</h2>
  <ul>
    <li><strong>Hermes is local.</strong> You run it. Your data stays on your machine.</li>
    <li><strong>API keys in env.</strong> Never commit them. <code>.env</code> in <code>.gitignore</code>.</li>
    <li><strong>Sandbox terminal calls.</strong> Use the workdir param to limit scope.</li>
    <li><strong>Channel allowlists.</strong> Don't let your bot talk to random guilds.</li>
    <li><strong>Rate limit free models.</strong> OpenRouter free tier is throttled.</li>
  </ul>

  <h2>📚 Further reading</h2>
  <ul>
    <li><a href="https://hermes-agent.nousresearch.com/docs" target="_blank" rel="noopener">Official Hermes docs</a></li>
    <li><a href="https://github.com/DonZzzilla/hermesDonZzz" target="_blank" rel="noopener">Our Hermes fork</a> (with backup scripts, custom skills)</li>
    <li><a href="{{ '/syllabus/' | relative_url }}">Back to syllabus</a></li>
  </ul>

</div>
