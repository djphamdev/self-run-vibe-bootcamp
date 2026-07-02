---
layout: default
title: "Tools & Pricing"
description: "Free and cheap alternatives to the AI dev stack taught at the LA TechWeek Vibe Coding Camp. Hermes, OpenRouter, Supabase, GitHub Pages, Cloudflare."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Their stack vs. ours · Updated July 2026</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">Tools & pricing</h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      The camp's stack assumes you'll pay for Cursor, ZeroDB, AIKit, and the
      AINative APIs. We use free alternatives that do the same job.
    </p>
  </div>
</div>

<div class="container" style="max-width: 1000px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">💰</span>
    <p>
      <strong>TL;DR:</strong> their stack = ~$30–$100/mo minimum.
      Our stack = $0 to start, ~$5/mo at scale, ~$15/yr for a custom domain.
      Same outcome, different price tag.
    </p>
  </div>

  <h2>🆚 Side-by-side comparison</h2>
  <table class="compare">
    <thead>
      <tr>
        <th>Layer</th>
        <th>Their stack</th>
        <th>Our stack</th>
        <th>Cost</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>AI IDE 1</td>
        <td>Windsurf</td>
        <td>Windsurf (free tier)</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>AI IDE 2</td>
        <td>Cursor</td>
        <td>Cursor (free tier) or <strong>Trae</strong> (full free)</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>CLI agent</td>
        <td>Claude Code</td>
        <td>Claude Code (BYO API key) or <strong>Hermes</strong></td>
        <td><span class="tag tag-free">$0–$5</span></td>
      </tr>
      <tr>
        <td>Vector memory</td>
        <td>ZeroDB</td>
        <td>Supabase pgvector / ChromaDB / Convex</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>UI components</td>
        <td>AIKit</td>
        <td>shadcn/ui / daisyUI / Mamba UI</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>Backend APIs</td>
        <td>AINative APIs</td>
        <td>Convex / Supabase / Cloudflare Workers</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>CLI tool</td>
        <td>AINative Code</td>
        <td>Open source CLI of your choice + Hermes</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>Multi-agent</td>
        <td>OpenClaw (alpha)</td>
        <td><strong>Hermes Agent</strong> + cron + skills</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>Model access</td>
        <td>AINative models</td>
        <td>OpenRouter (free tier) or BYO key</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>Hosting</td>
        <td>AINative cloud</td>
        <td>GitHub Pages + Cloudflare</td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>Domain</td>
        <td>(included)</td>
        <td>Cloudflare Registrar (at-cost)</td>
        <td><span class="tag tag-cheap">~$10/yr</span></td>
      </tr>
    </tbody>
  </table>

  <h2 id="ides">🤖 AI IDEs (free or freemium)</h2>

  <div class="grid grid-2">
    <div class="card">
      <h3>Windsurf <span class="tag tag-free">Free</span></h3>
      <p>Codeium's VSCode fork. Cascade agent, fast, free tier generous.
      What the camp uses.</p>
      <div class="tags">
        <span class="tag">VSCode-based</span>
        <span class="tag">Cascade agent</span>
      </div>
    </div>
    <div class="card">
      <h3>Cursor <span class="tag tag-cheap">Free + $20/mo Pro</span></h3>
      <p>Most popular. Free tier exists, Pro unlocks more models.
      Composer + Agent mode is great.</p>
      <div class="tags">
        <span class="tag">VSCode-based</span>
        <span class="tag">Composer</span>
      </div>
    </div>
    <div class="card">
      <h3>Trae <span class="tag tag-free">Free</span></h3>
      <p>ByteDance's answer to Cursor. Fully free, surprisingly good.
      Best free option in 2026.</p>
      <div class="tags">
        <span class="tag">VSCode-based</span>
        <span class="tag">Agent mode</span>
      </div>
    </div>
    <div class="card">
      <h3>Claude Code <span class="tag tag-free">BYO API</span></h3>
      <p>CLI-native. Plan mode, multi-file, agentic. Free if you bring your own
      Anthropic or OpenRouter key.</p>
      <div class="tags">
        <span class="tag">CLI</span>
        <span class="tag">Agentic</span>
      </div>
    </div>
    <div class="card">
      <h3>Kiro <span class="tag tag-free">Preview</span></h3>
      <p>AWS's spec-driven IDE. Free during preview. Good for greenfield projects.</p>
      <div class="tags">
        <span class="tag">VSCode-based</span>
        <span class="tag">Spec-driven</span>
      </div>
    </div>
    <div class="card">
      <h3>AINative IDE <span class="tag tag-free">OSS</span></h3>
      <p>The camp's open-source option. Browser-based. Worth a look.</p>
      <div class="tags">
        <span class="tag">Browser</span>
        <span class="tag">OSS</span>
      </div>
    </div>
    <div class="card">
      <h3>AntiGravity <span class="tag tag-free">Free tier</span></h3>
      <p>Agentic workspace, free tier. Newer, less docs.</p>
      <div class="tags">
        <span class="tag">Agentic</span>
        <span class="tag">Workspace</span>
      </div>
    </div>
    <div class="card">
      <h3>Google CLI <span class="tag tag-free">Free</span></h3>
      <p>Google's Gemini CLI. Free with Google account. Surprisingly capable.</p>
      <div class="tags">
        <span class="tag">CLI</span>
        <span class="tag">Gemini</span>
      </div>
    </div>
  </div>

  <h2 id="infra">🧱 Infrastructure (free tiers)</h2>

  <h3>Vector memory</h3>
  <div class="price-row">
    <span class="name">Supabase pgvector</span>
    <span class="tag tag-free">FREE · 500MB · 50k rows</span>
  </div>
  <div class="price-row">
    <span class="name">ChromaDB (self-hosted)</span>
    <span class="tag tag-free">FREE · Unlimited</span>
  </div>
  <div class="price-row">
    <span class="name">Convex vector search</span>
    <span class="tag tag-free">FREE · 1GB · Generous</span>
  </div>
  <div class="price-row">
    <span class="name">FAISS (Meta, local)</span>
    <span class="tag tag-free">FREE · Unlimited</span>
  </div>
  <div class="price-row">
    <span class="name">ZeroDB (theirs)</span>
    <span class="tag tag-steep">$ ?/mo</span>
  </div>

  <h3>Backend</h3>
  <div class="price-row">
    <span class="name">Convex</span>
    <span class="tag tag-free">FREE · 1M function calls/mo</span>
  </div>
  <div class="price-row">
    <span class="name">Supabase</span>
    <span class="tag tag-free">FREE · 500MB DB · 50k MAU</span>
  </div>
  <div class="price-row">
    <span class="name">Cloudflare Workers</span>
    <span class="tag tag-free">FREE · 100k req/day</span>
  </div>
  <div class="price-row">
    <span class="name">AINative APIs</span>
    <span class="tag tag-steep">$ ?/mo</span>
  </div>

  <h3>UI components</h3>
  <div class="price-row">
    <span class="name">shadcn/ui</span>
    <span class="tag tag-free">FREE · MIT · Copy-paste</span>
  </div>
  <div class="price-row">
    <span class="name">daisyUI</span>
    <span class="tag tag-free">FREE · MIT</span>
  </div>
  <div class="price-row">
    <span class="name">Mamba UI</span>
    <span class="tag tag-free">FREE · MIT</span>
  </div>
  <div class="price-row">
    <span class="name">AIKit (theirs)</span>
    <span class="tag tag-steep">$ ?/mo</span>
  </div>

  <h3>LLM access</h3>
  <div class="price-row">
    <span class="name">OpenRouter free models</span>
    <span class="tag tag-free">FREE · Rate-limited</span>
  </div>
  <div class="price-row">
    <span class="name">OpenRouter paid</span>
    <span class="tag tag-cheap">$5–$20/mo · BYO budget</span>
  </div>
  <div class="price-row">
    <span class="name">Ollama (local)</span>
    <span class="tag tag-free">FREE · Run on your machine</span>
  </div>
  <div class="price-row">
    <span class="name">AINative models</span>
    <span class="tag tag-steep">$ ?/mo</span>
  </div>

  <h2>☁️ Hosting & domains</h2>
  <div class="price-row">
    <span class="name">GitHub Pages</span>
    <span class="tag tag-free">FREE · Unlimited static sites</span>
  </div>
  <div class="price-row">
    <span class="name">Cloudflare Pages</span>
    <span class="tag tag-free">FREE · 500 builds/mo</span>
  </div>
  <div class="price-row">
    <span class="name">Vercel</span>
    <span class="tag tag-free">FREE · Hobby tier</span>
  </div>
  <div class="price-row">
    <span class="name">Netlify</span>
    <span class="tag tag-free">FREE · 100GB bandwidth/mo</span>
  </div>
  <div class="price-row">
    <span class="name">Cloudflare Registrar (domains)</span>
    <span class="tag tag-cheap">~$10/yr · At-cost, no markup</span>
  </div>
  <div class="price-row">
    <span class="name">Namecheap (alternative)</span>
    <span class="tag tag-cheap">~$10–$15/yr</span>
  </div>

  <h2>🤖 Multi-agent (our OpenClaw replacement)</h2>
  <table class="compare">
    <thead>
      <tr><th>Feature</th><th>OpenClaw</th><th>Hermes Agent</th></tr>
    </thead>
    <tbody>
      <tr>
        <td>Run agents locally</td>
        <td class="yes">✓</td>
        <td class="yes">✓</td>
      </tr>
      <tr>
        <td>Peer-to-peer coordination</td>
        <td class="yes">✓ (alpha)</td>
        <td class="mid">~ (via cron + shared memory)</td>
      </tr>
      <tr>
        <td>Distributed AI collaboration</td>
        <td class="yes">✓ (experimental)</td>
        <td class="mid">~ (multiple Hermes instances + webhook)</td>
      </tr>
      <tr>
        <td>Private AI networks</td>
        <td class="yes">✓</td>
        <td class="yes">✓ (self-hosted)</td>
      </tr>
      <tr>
        <td>Skills / plugins</td>
        <td class="mid">~</td>
        <td class="yes">✓ (first-class)</td>
      </tr>
      <tr>
        <td>Cron jobs</td>
        <td class="no">✗</td>
        <td class="yes">✓ (built-in scheduler)</td>
      </tr>
      <tr>
        <td>Multi-channel (Discord/Telegram)</td>
        <td class="no">✗</td>
        <td class="yes">✓ (built-in)</td>
      </tr>
      <tr>
        <td>Production-ready</td>
        <td class="no">✗ (alpha)</td>
        <td class="yes">✓ (active development)</td>
      </tr>
      <tr>
        <td>Cost</td>
        <td>free (alpha)</td>
        <td><span class="tag tag-free">free</span></td>
      </tr>
    </tbody>
  </table>

  <div class="callout">
    <span class="icon-c">🎯</span>
    <p><strong>Bottom line:</strong> OpenClaw is an interesting experiment.
    Hermes is the same idea in production-ready form. We use Hermes.</p>
  </div>

  <h2>📊 Total cost summary</h2>
  <table class="compare">
    <thead>
      <tr><th>Scenario</th><th>Their stack</th><th>Our stack</th></tr>
    </thead>
    <tbody>
      <tr>
        <td>Just starting (week 1)</td>
        <td><span class="tag tag-steep">$20–$30/mo</span></td>
        <td><span class="tag tag-free">$0</span></td>
      </tr>
      <tr>
        <td>Active building (month 1–3)</td>
        <td><span class="tag tag-steep">$50–$100/mo</span></td>
        <td><span class="tag tag-cheap">$0–$5/mo</span></td>
      </tr>
      <tr>
        <td>Shipped product (year 1)</td>
        <td><span class="tag tag-steep">$600–$1,200/yr</span></td>
        <td><span class="tag tag-cheap">~$10–$60/yr</span></td>
      </tr>
    </tbody>
  </table>

  <p>You do the math. Same outcome, ~$500+/yr difference. That's a domain, a
  coffee budget for a year, or a side hustle's seed money.</p>

</div>
