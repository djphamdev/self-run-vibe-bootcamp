---
layout: default
title: "Syllabus"
description: "The full 8-module AI-native vibe coding curriculum, reverse-engineered from the LA TechWeek Vibe Coding Camp."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Full curriculum · Self-paced · Free</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">The syllabus</h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      Eight modules. Twenty-something hours. One shipped AI-native app at the end.
      This is the curriculum we wish existed before the camp in October.
    </p>
  </div>
</div>

<div class="container" style="max-width: 900px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">📋</span>
    <p>
      <strong>Source:</strong> reverse-engineered from the LA TechWeek Vibe Coding Camp (Oct 15, 2026),
      hosted by AINative Studio. We kept the spirit and structure, swapped out the paid tools
      for free/open alternatives, and replaced OpenClaw with Hermes Agent.
    </p>
  </div>

  <h2>📅 Schedule (suggested)</h2>
  <div class="timeline">
    <div class="tl-item">
      <div class="tl-time">WEEK 1 · ~2 hrs</div>
      <div class="tl-title">Module 0: Setup</div>
      <div class="tl-desc">Install the free stack. Get Hermes talking to OpenRouter. Verify GitHub Pages deploys.</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 1 · ~2 hrs</div>
      <div class="tl-title">Module 1: Prompting patterns</div>
      <div class="tl-desc">Structured vs. unstructured pair programming. How to think with a model, not at it.</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 2 · ~3 hrs</div>
      <div class="tl-title">Module 2: AI IDE tour</div>
      <div class="tl-desc">Windsurf, Cursor, Claude Code, Kiro, Trae, AntiGravity, AINative. Build the same thing in each. Compare.</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 2 · ~2 hrs</div>
      <div class="tl-title">Module 3: Vector memory</div>
      <div class="tl-desc">Free Supabase pgvector, ChromaDB, or Convex vectors. Build a RAG pipeline.</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 3 · ~2 hrs</div>
      <div class="tl-title">Module 4: UI components</div>
      <div class="tl-desc">shadcn/ui, daisyUI, Mamba UI. Copy-paste a beautiful front-end in 20 minutes.</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 3 · ~4 hrs</div>
      <div class="tl-title">Module 5: Hermes Agent</div>
      <div class="tl-desc">Skills, plugins, cron, sub-agents, Discord/Telegram. The real agentic runtime.</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 4 · ~3 hrs</div>
      <div class="tl-title">Module 6: Multi-agent</div>
      <div class="tl-desc">Coordinate agents. Cron + skills = real production workflow. (Replaces OpenClaw.)</div>
    </div>
    <div class="tl-item">
      <div class="tl-time">WEEK 4 · ~4 hrs</div>
      <div class="tl-title">Module 7: Ship it</div>
      <div class="tl-desc">Build the AI-native app from the syllabus. Deploy to GitHub Pages. Get a real URL. Show it off.</div>
    </div>
  </div>

  <hr>

  <h2>📚 Module 0: Setup <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> a working free stack.</p>
  <ul>
    <li>☐ GitHub account + SSH key</li>
    <li>☐ OpenRouter account + API key</li>
    <li>☐ Hermes Agent installed (laptop or Pi)</li>
    <li>☐ One AI IDE installed (Cursor or Trae recommended)</li>
    <li>☐ A test repo with GitHub Pages enabled</li>
    <li>☐ Verified: <code>hermes chat "hi"</code> returns a response</li>
  </ul>
  <p><a href="{{ '/start/' | relative_url }}">→ Full setup walkthrough</a></p>

  <h2>🧠 Module 1: Prompting patterns <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> learn to think with a model.</p>
  <h3>Patterns to master</h3>
  <ul>
    <li><strong>Show, don't tell</strong> — give an example, not a rule</li>
    <li><strong>Few-shot</strong> — 2-3 examples > a 500-word spec</li>
    <li><strong>Plan first</strong> — "outline your approach before coding"</li>
    <li><strong>Constraints</strong> — "no dependencies, vanilla JS, &lt;100 lines"</li>
    <li><strong>Critique loop</strong> — "review your own output, then improve"</li>
    <li><strong>Persona</strong> — "you are a senior backend engineer who ships to prod"</li>
  </ul>
  <h3>Exercises</h3>
  <ol>
    <li>Build the same FizzBuzz with 3 different prompting styles. Compare.</li>
    <li>Take a vague task ("build a todo app"). Add 5 different constraints. Build all 5.</li>
    <li>Have the model critique its own code 3 times. Was it better after?</li>
  </ol>

  <h2 id="ides">🛠 Module 2: AI IDE tour <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> experience 5+ AI coding environments on the same task.</p>
  <h3>IDEs to try</h3>
  <ul>
    <li><strong>Windsurf</strong> — Cascade agent, free tier</li>
    <li><strong>Cursor</strong> — Composer + Agent mode, free tier</li>
    <li><strong>Trae</strong> — ByteDance's free Cursor</li>
    <li><strong>Claude Code</strong> — CLI agentic coding, free with API</li>
    <li><strong>Kiro</strong> — AWS spec-driven IDE, free preview</li>
    <li><strong>AntiGravity</strong> — agentic workspace, free tier</li>
    <li><strong>AINative IDE</strong> — the camp's open-source option</li>
  </ul>
  <h3>Exercise</h3>
  <p>Build a markdown blog with three.js animations in each IDE. Time yourself.
  Compare:</p>
  <ul>
    <li>Setup friction</li>
    <li>Speed to first working version</li>
    <li>Code quality of output</li>
    <li>How it handles "review this and improve"</li>
    <li>Multi-file editing</li>
  </ul>

  <h2>🧱 Module 3: Vector memory <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> build a working RAG pipeline.</p>
  <h3>Free options</h3>
  <ul>
    <li><strong>Supabase pgvector</strong> — Postgres extension, free tier generous</li>
    <li><strong>ChromaDB</strong> — runs locally, embed-and-go</li>
    <li><strong>Convex vectors</strong> — if you're using Convex for backend</li>
    <li><strong>FAISS</strong> — Meta's library, runs anywhere</li>
  </ul>
  <h3>Exercise</h3>
  <ol>
    <li>Pick 5 articles from your favorite blog.</li>
    <li>Embed them. Store in your vector DB of choice.</li>
    <li>Build a "ask the blog" interface. Query → top-3 chunks → answer.</li>
    <li>Compare retrieval quality across the 3 DBs.</li>
  </ol>

  <h2>🎨 Module 4: UI components <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> ship a beautiful front-end without designing it.</p>
  <h3>Free component libraries</h3>
  <ul>
    <li><strong>shadcn/ui</strong> — copy-paste, fully owned, Tailwind-based</li>
    <li><strong>daisyUI</strong> — Tailwind plugin, lots of themes</li>
    <li><strong>Mamba UI</strong> — Tailwind, free, no attribution</li>
    <li><strong>NextUI / HeroUI</strong> — beautiful, free, React</li>
    <li><strong>Radix Primitives</strong> — unstyled, accessible</li>
  </ul>
  <h3>Exercise</h3>
  <p>Take the blog app from Module 3. Add:</p>
  <ul>
    <li>A landing page with hero, features, CTA</li>
    <li>A search interface with live results</li>
    <li>A dark-mode toggle (joke's on us — we're dark-mode only)</li>
  </ul>

  <h2>🤖 Module 5: Hermes Agent <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> learn the agentic runtime.</p>
  <p><a href="{{ '/hermes/' | relative_url }}">→ Full Hermes guide</a></p>
  <h3>Topics</h3>
  <ul>
    <li>Skills — modular capabilities the agent can invoke</li>
    <li>Plugins — extend the runtime</li>
    <li>Cron jobs — schedule anything</li>
    <li>Sub-agents — delegate to specialized agents</li>
    <li>Memory — persistent state across sessions</li>
    <li>Multi-channel — Discord, Telegram, CLI</li>
  </ul>
  <h3>Exercise</h3>
  <p>Build a "personal research assistant" that:</p>
  <ol>
    <li>Wakes up every morning at 9am (cron)</li>
    <li>Searches the web for your topics (skill)</li>
    <li>Summarizes the top 5 results (LLM)</li>
    <li>Posts to Discord (multi-channel)</li>
    <li>Stores results in vector memory for later search (memory)</li>
  </ol>

  <h2>🔁 Module 6: Multi-agent workflows <span class="tag tag-free">$0</span></h2>
  <p><strong>Goal:</strong> coordinate multiple agents.</p>
  <h3>Why this replaces OpenClaw</h3>
  <p>OpenClaw is "peer-to-peer AI agent runtime". Cool idea, alpha product.
  Hermes already does the practical version: multiple agents coordinated via
  cron, shared memory, and skills. You get the same end result without the
  experimental risk.</p>
  <h3>Exercise</h3>
  <p>Build a "content pipeline":</p>
  <ol>
    <li><strong>Researcher agent</strong> — finds and saves articles</li>
    <li><strong>Writer agent</strong> — turns articles into blog posts</li>
    <li><strong>Critic agent</strong> — reviews and improves</li>
    <li><strong>Publisher agent</strong> — posts to GitHub Pages repo</li>
  </ol>
  <p>Each runs on its own cron schedule, reads/writes shared memory, and you can
  monitor the whole thing from Discord.</p>

  <h2>🚀 Module 7: Ship it <span class="tag tag-free">$0–$5</span></h2>
  <p><strong>Goal:</strong> a working AI-native app on the open web.</p>
  <h3>Options</h3>
  <ul>
    <li><a href="{{ '/projects/' | relative_url }}">→ See project ideas</a></li>
    <li>Bring your own idea and vibe-code it live</li>
  </ul>
  <h3>Deliverable</h3>
  <p>A deployed app with:</p>
  <ul>
    <li>Custom domain (or <code>*.github.io</code>)</li>
    <li>Vector memory for at least one feature</li>
    <li>Handsome dark-mode UI</li>
    <li>At least one agent (Hermes) automating something in the background</li>
    <li>Source on GitHub, public</li>
  </ul>

  <h2>🎯 What you'll leave with</h2>
  <ul>
    <li>✓ A working AI-native project (or validated prototype)</li>
    <li>✓ Experience using 5+ AI IDEs on the same task</li>
    <li>✓ A mental model for tool selection in 2026</li>
    <li>✓ A repeatable workflow for AI pair programming</li>
    <li>✓ Clarity on when to use which platform</li>
    <li>✓ Rules for your IDE or CLI Coding tool</li>
    <li>✓ Skills for Hermes Agent, Claude Code, and friends</li>
  </ul>

  <div class="callout">
    <span class="icon-c">🎓</span>
    <p><strong>Reminder:</strong> this is about learning how to <em>think</em>, not just copy commands.
    The tools will change. The workflow won't.</p>
  </div>

</div>
