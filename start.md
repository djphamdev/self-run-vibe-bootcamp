---
layout: default
title: "Start Here"
description: "Set up your free AI-native dev stack in under an hour. Hermes Agent, OpenRouter, GitHub Pages, and the rest."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 0 · 1 hour · $0</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">Start here.</h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      Five minutes to read, one hour to set up. By the end you have a working
      AI-native dev environment on the open web for <strong>free</strong>.
    </p>

    <div class="callout">
      <span class="icon-c">🎯</span>
      <p><strong>Goal of this page:</strong> get you from zero to "I just shipped a
      thing" in the shortest path. Skip steps you've already done.</p>
    </div>
  </div>
</div>

<div class="container" style="max-width: 760px; padding-bottom: 60px;">

  <h2>📋 The stack (everything free to start)</h2>
  <table class="compare">
    <thead>
      <tr>
        <th>Layer</th>
        <th>Tool</th>
        <th>Cost</th>
        <th>Why</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>LLM routing</td>
        <td>OpenRouter (free models)</td>
        <td><span class="yes">$0</span></td>
        <td>One API, many free models. No vendor lock-in.</td>
      </tr>
      <tr>
        <td>Agent runtime</td>
        <td>Hermes Agent</td>
        <td><span class="yes">$0</span></td>
        <td>Self-hosted agentic runtime. Skills, plugins, cron, sub-agents.</td>
      </tr>
      <tr>
        <td>AI IDE</td>
        <td>Windsurf Free / Cursor Free / Claude Code / Trae</td>
        <td><span class="yes">$0</span></td>
        <td>Compare live. Use whichever fits the task.</td>
      </tr>
      <tr>
        <td>Vector memory</td>
        <td>Supabase pgvector (free) or ChromaDB local</td>
        <td><span class="yes">$0</span></td>
        <td>ZeroDB alternative. Embeddings, RAG, retrieval.</td>
      </tr>
      <tr>
        <td>UI components</td>
        <td>shadcn/ui / daisyUI / Mamba UI</td>
        <td><span class="yes">$0</span></td>
        <td>AIKit alternative. Copy-paste React components.</td>
      </tr>
      <tr>
        <td>Hosting</td>
        <td>GitHub Pages</td>
        <td><span class="yes">$0</span></td>
        <td>Static hosting with custom domain support.</td>
      </tr>
      <tr>
        <td>Domain</td>
        <td>Cloudflare Registrar</td>
        <td><span class="yes">~$10/yr</span></td>
        <td>At-cost domains. No markup.</td>
      </tr>
      <tr>
        <td>Backend</td>
        <td>Convex (free tier) or Supabase</td>
        <td><span class="yes">$0</span></td>
        <td>Realtime DB, serverless functions, free tier generous.</td>
      </tr>
      <tr>
        <td>Peer-to-peer</td>
        <td>Hermes cron + WebSockets (instead of OpenClaw)</td>
        <td><span class="yes">$0</span></td>
        <td>Decentralized-ish. Schedule agents, they coordinate.</td>
      </tr>
    </tbody>
  </table>

  <h2>🚀 Setup, in order</h2>

  <h3>Step 1: Create a GitHub account (if you don't have one)</h3>
  <p>
    You're on GitHub Pages, so you need one anyway. Free for public repos, $4/mo for
    private if you need that.
  </p>
  <div class="prompt">https://github.com/signup</div>

  <h3>Step 2: Get an OpenRouter API key</h3>
  <p>OpenRouter is one API, many free models. Sign up, get a key, put some free credits on it (they give you a tiny starter).</p>
  <div class="prompt">https://openrouter.ai/keys</div>
  <p>Set the env var in your shell. Don't commit it to git.</p>
  <div class="prompt">export OPENROUTER_API_KEY="sk-or-v1-..."</div>
  <p><strong>Free models that work for vibe coding:</strong></p>
  <ul>
    <li><code>qwen/qwen-2.5-coder-32b-instruct:free</code> — best free coding model, usually</li>
    <li><code>google/gemini-2.0-flash-exp:free</code> — fast, multimodal</li>
    <li><code>meta-llama/llama-3.3-70b-instruct:free</code> — solid general</li>
    <li><code>mistralai/mistral-small-3.1-24b-instruct:free</code> — good at structured output</li>
  </ul>
  <div class="callout">
    <span class="icon-c">💡</span>
    <p><strong>Heads up:</strong> "free" models on OpenRouter have rate limits and can be slow during peak hours. For real work, set up a small budget ($5/mo goes a long way).</p>
  </div>

  <h3>Step 3: Install Hermes Agent</h3>
  <p>Hermes is a self-hosted agentic runtime. You can run it on a Pi, a laptop, a VPS, or even inside GitHub Actions.</p>
  <div class="prompt">git clone https://github.com/DonZzzilla/hermesDonZzz.git ~/projects/hermes
cd ~/projects/hermes
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
hermes init  # creates ~/.hermes/ with config, skills, memories</div>
  <p>Configure it to use OpenRouter:</p>
  <div class="prompt">cat >> ~/.hermes/config.yaml <<'EOF'
providers:
  openrouter:
    api_key: "${OPENROUTER_API_KEY}"
    base_url: "https://openrouter.ai/api/v1"
    default_model: "qwen/qwen-2.5-coder-32b-instruct:free"
EOF</div>
  <p>Smoke test:</p>
  <div class="prompt">hermes chat "hi, what's 2+2?"</div>
  <p>If you get "4" back, you're up. 🎉</p>

  <h3>Step 4: Pick an AI IDE</h3>
  <p>You can use them all. Here's the quick guide:</p>
  <table class="compare">
    <thead>
      <tr><th>IDE</th><th>Free?</th><th>Best for</th></tr>
    </thead>
    <tbody>
      <tr><td><strong>Windsurf</strong></td><td><span class="yes">Yes (limited)</span></td><td>VSCode vibes, Cascade agent</td></tr>
      <tr><td><strong>Cursor</strong></td><td><span class="yes">Yes (limited)</span></td><td>Forked VSCode, Agent mode, Composer</td></tr>
      <tr><td><strong>Claude Code</strong></td><td><span class="yes">Yes (with API)</span></td><td>CLI-native, agentic, plan mode</td></tr>
      <tr><td><strong>Trae</strong></td><td><span class="yes">Yes</span></td><td>ByteDance's free Cursor</td></tr>
      <tr><td><strong>Kiro</strong></td><td><span class="yes">Preview</span></td><td>AWS, spec-driven</td></tr>
      <tr><td><strong>AINative IDE</strong></td><td><span class="yes">Yes (OSS)</span></td><td>Their open-source one, browser-based</td></tr>
      <tr><td><strong>AntiGravity</strong></td><td><span class="yes">Free tier</span></td><td>Agentic workspace</td></tr>
    </tbody>
  </table>
  <p><strong>Recommendation:</strong> Start with <strong>Cursor</strong> or <strong>Trae</strong> (free,
  best UX). Keep <strong>Claude Code</strong> in your terminal for the agentic flow.
  Use <strong>Hermes</strong> when you need scheduling, multi-step automation, or anything 24/7.</p>

  <h3>Step 5: Set up GitHub Pages</h3>
  <p>Create a repo, push a static site, turn on Pages. Done in 2 minutes.</p>
  <div class="prompt"># Use the GitHub UI or the CLI:
gh repo create my-vibe-app --public --source=. --push --remote
gh repo edit my-vibe-app --enable-pages --pages-source=main

# Or use the UI: Settings → Pages → Source: main / root</div>
  <p>Your site will be live at <code>https://YOUR_USER.github.io/my-vibe-app</code>.</p>

  <h3>Step 6 (optional): Custom domain via Cloudflare</h3>
  <ol>
    <li>Buy a domain on Cloudflare Registrar (~$10/yr, at-cost)</li>
    <li>Add a <code>CNAME</code> record pointing to <code>YOUR_USER.github.io</code></li>
    <li>In your GitHub repo Settings → Pages → Custom domain, enter the domain</li>
    <li>Enable "Enforce HTTPS"</li>
  </ol>
  <p>Total cost: domain only (~$10/yr). GitHub Pages is free, Cloudflare DNS is free.</p>

  <h3>Step 7 (optional): Backend with Convex</h3>
  <p>Convex is a realtime serverless backend with a generous free tier. Great for
  vibe coding because you can iterate schema and functions without redeploying.</p>
  <div class="prompt">npm install convex
npx convex init
npx convex dev  # starts dev server</div>
  <p>Free tier: 1M function calls/mo, 0.5 GB storage. Enough for most side projects.</p>

  <h2>✅ Setup checklist</h2>
  <ul>
    <li>☐ GitHub account</li>
    <li>☐ OpenRouter API key</li>
    <li>☐ Hermes Agent installed and tested</li>
    <li>☐ At least one AI IDE installed</li>
    <li>☐ GitHub Pages enabled on a test repo</li>
    <li>☐ (Optional) Custom domain on Cloudflare</li>
    <li>☐ (Optional) Convex backend</li>
  </ul>

  <h2>🎓 What's next?</h2>
  <p>You have the stack. Now let's actually use it.</p>
  <div class="hero-actions" style="margin-top: 20px;">
    <a href="{{ '/syllabus/' | relative_url }}" class="btn btn-primary">📚 Open the syllabus</a>
    <a href="{{ '/hermes/' | relative_url }}" class="btn btn-ghost">🤖 Learn Hermes first</a>
  </div>

</div>
