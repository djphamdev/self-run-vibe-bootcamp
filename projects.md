---
layout: default
title: "Projects"
description: "Project ideas to build during the bootcamp. Pick one, vibe-code it, ship it."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 7 · Pick one · Ship it</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">Projects</h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      By the end of the bootcamp you'll have one of these shipped. Pick one and
      vibe-code it, or bring your own. The point is to have something real
      with your name on it.
    </p>
  </div>
</div>

<div class="container" style="max-width: 1000px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">🚀</span>
    <p>
      <strong>The camp's project:</strong> "Build a small AI-native app from
      scratch. Use ZeroDB for memory + embeddings, wire UI using AIKit."
      <br><br>
      <strong>Ours:</strong> same idea, free stack. Pick one below or bring your own.
    </p>
  </div>

  <h2>🌱 Beginner (2–4 hrs)</h2>

  <div class="grid grid-2">
    <div class="card">
      <div class="mono accent">// P1</div>
      <h3>Personal blog with semantic search</h3>
      <p>Static site (Jekyll/Astro) on GitHub Pages. Embed your old posts in
      ChromaDB. Search "what did I write about X?" → returns relevant posts
      with snippets.</p>
      <div class="tags">
        <span class="tag">Jekyll</span>
        <span class="tag">ChromaDB</span>
        <span class="tag">Embeddings</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P2</div>
      <h3>Daily quote + LLM reflection</h3>
      <p>GitHub Pages. Cron fetches a quote, asks LLM to write a 3-sentence
      reflection, posts to a daily page. Build a year of "thoughts" automatically.</p>
      <div class="tags">
        <span class="tag">Cron</span>
        <span class="tag">GitHub Actions</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P3</div>
      <h3>Markdown cheat sheet generator</h3>
      <p>Static site. User picks a topic, LLM generates a personalized cheat
      sheet. Save to localStorage. Add share-as-URL.</p>
      <div class="tags">
        <span class="tag">Vanilla JS</span>
        <span class="tag">localStorage</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P4</div>
      <h3>RSS-to-podcast-episode</h3>
      <p>Pick an RSS feed. Cron fetches new posts. LLM summarizes. TTS turns
      summary into audio. Host MP3s on GitHub Pages. Tiny podcast.</p>
      <div class="tags">
        <span class="tag">TTS</span>
        <span class="tag">Cron</span>
        <span class="tag">RSS</span>
      </div>
    </div>
  </div>

  <h2>🌿 Intermediate (4–8 hrs)</h2>

  <div class="grid grid-2">
    <div class="card">
      <div class="mono accent">// P5</div>
      <h3>Ask-my-repo</h3>
      <p>GitHub Pages + Convex backend. Indexes any GitHub repo. "What does
      the auth flow do?" → answer grounded in actual code. RAG for your
      own projects.</p>
      <div class="tags">
        <span class="tag">RAG</span>
        <span class="tag">Convex</span>
        <span class="tag">Code search</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P6</div>
      <h3>Hacker News digest</h3>
      <p>Cron scrapes HN hourly. LLM scores stories by your interests. Daily
      digest at 8am. Discord notification with top 5. Free forever.</p>
      <div class="tags">
        <span class="tag">Cron</span>
        <span class="tag">Web search</span>
        <span class="tag">Discord</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P7</div>
      <h3>Multi-agent content pipeline</h3>
      <p>4 Hermes agents: researcher → writer → critic → publisher. They
      collaborate via shared memory. Output: weekly blog post on your
      chosen topic.</p>
      <div class="tags">
        <span class="tag">Multi-agent</span>
        <span class="tag">Hermes</span>
        <span class="tag">Memory</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P8</div>
      <h3>Flight tracker for specific dates</h3>
      <p>Hermes cron checks flight prices for your dates (non-stop only). If price drops below threshold, alerts via Discord/Telegram with booking link. Free forever. Perfect for planning trips.</p>
      <div class="tags">
        <span class="tag">Cron</span>
        <span class="tag">Flights</span>
        <span class="tag">Alert</span>
      </div>
    </div>
  </div>

  <h2>🌳 Advanced (8+ hrs)</h2>

  <div class="grid grid-2">
    <div class="card">
      <div class="mono accent">// P9</div>
      <h3>AI-native wiki with vector search</h3>
      <p>Like MediaWiki but with embeddings. Every page is searchable by
      meaning. Convex backend, shadcn/ui front-end. Open-source.</p>
      <div class="tags">
        <span class="tag">Convex</span>
        <span class="tag">Embeddings</span>
        <span class="tag">shadcn/ui</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P10</div>
      <h3>Discord bot that runs the bootcamp</h3>
      <p>A Hermes agent with a "bootcamp" skill. Asks you questions,
      tracks your progress, celebrates milestones. The bootcamp itself,
      in Discord form.</p>
      <div class="tags">
        <span class="tag">Discord</span>
        <span class="tag">Hermes</span>
        <span class="tag">Meta</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P11</div>
      <h3>Decentralized research network</h3>
      <p>Multiple Hermes instances (yours, your friends', a friend's Pi) that
      share findings via a shared Convex backend. OpenClaw-style coordination
      without OpenClaw.</p>
      <div class="tags">
        <span class="tag">Multi-agent</span>
        <span class="tag">Distributed</span>
        <span class="tag">Convex</span>
      </div>
    </div>
    <div class="card">
      <div class="mono accent">// P12</div>
      <h3>Real-time LLM eval harness</h3>
      <p>Compare outputs from 5+ free models on the same prompt. Side-by-side
      UI. Vote on which is best. Public leaderboard. Live forever on
      GitHub Pages.</p>
      <div class="tags">
        <span class="tag">Eval</span>
        <span class="tag">Comparison</span>
        <span class="tag">OpenRouter</span>
      </div>
    </div>
  </div>

  <h2>🎯 How to choose</h2>
  <p>Pick something that solves a problem <em>you</em> have. The motivation
  to finish is 10x stronger when it's personal.</p>
  <p>Don't pick something too big. "Vibe coding" is iterative, not heroic.
  Ship a v0, then improve.</p>
  <p>Don't pick something that requires users to be valuable. Build a tool
  for <em>you</em> first.</p>

  <h2>📦 Project template</h2>
  <p>Each project should have:</p>
  <ul>
    <li>☐ GitHub repo (public, MIT or your choice)</li>
    <li>☐ README with one-paragraph pitch + screenshots</li>
    <li>☐ Live URL (GitHub Pages or your domain)</li>
    <li>☐ At least one AI-native feature (RAG, agent, embeddings)</li>
    <li>☐ Dark mode (obviously)</li>
    <li>☐ A "Built with" badge crediting the bootcamp</li>
  </ul>

  <h2>🏆 Share your work</h2>
  <p>Done? Open a PR to <a href="https://github.com/{{ site.github_username }}/{{ site.github_repo }}" target="_blank" rel="noopener">this repo</a>
  adding your project to <code>/projects/community/</code>. We'll feature
  the best ones on the front page.</p>

</div>
