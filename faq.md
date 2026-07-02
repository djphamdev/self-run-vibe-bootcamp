---
layout: default
title: "FAQ"
description: "Common questions about the Self-Run Vibe Bootcamp, the free stack, and Hermes Agent."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Common questions · Updated July 2026</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">FAQ</h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      Quick answers to the most common questions.
    </p>
  </div>
</div>

<div class="container" style="max-width: 800px; padding-bottom: 60px;">

  <h2>🎓 About the bootcamp</h2>

  <h3>Is this the same as the LA TechWeek Vibe Coding Camp?</h3>
  <p>
    No. The LA TechWeek Vibe Coding Camp is an in-person event on
    October 15, 2026 in Los Angeles, hosted by AINative Studio. This
    is a self-directed, online, free alternative with the same
    curriculum shape but a different (free) tool stack.
  </p>

  <h3>Will I get a certificate?</h3>
  <p>
    No. There are no certificates, badges, or credentials. The proof is
    in what you ship. A live URL is worth more than any PDF.
  </p>

  <h3>How long does it take?</h3>
  <p>
    Self-paced. The full curriculum is ~20 hours of focused work. Some
    people bang it out in a weekend. Some take a month. Some take 3
    months and ship a real side business. It's yours.
  </p>

  <h3>Do I need to know how to code?</h3>
  <p>
    You need to be able to read code and follow terminal instructions.
    "Vibe coding" means you let the model write most of it, but you
    still need to know what good code looks like. If you've never
    written a <code>for</code> loop, start with a JS basics tutorial
    first.
  </p>

  <h3>What do I get out of it?</h3>
  <p>
    By the end you have: a working AI-native project on the open web,
    experience with 5+ AI IDEs on the same task, a mental model for tool
    selection, a repeatable workflow for AI pair programming, and a
    working knowledge of Hermes Agent for agentic automation.
  </p>

  <hr>

  <h2>🛠 About the tools</h2>

  <h3>Why Hermes Agent instead of OpenClaw?</h3>
  <p>
    OpenClaw is an interesting peer-to-peer agent runtime, but it's
    alpha. Hermes is the same idea in production-ready form: it has
    skills, plugins, cron, sub-agents, multi-channel, and a real
    community. We use it in production for cron jobs, Discord bots,
    and content pipelines. Same outcome, fewer surprises.
  </p>

  <h3>Are free models actually good enough?</h3>
  <p>
    Surprisingly, yes. The free models on OpenRouter (Qwen 2.5 Coder,
    Gemini 2.0 Flash, Llama 3.3) can match or beat paid models on
    coding tasks. They have rate limits and can be slow at peak hours,
    but for vibe coding they're great. The free tier is also how you
    learn what to actually pay for later.
  </p>

  <h3>What if I already pay for Cursor Pro?</h3>
  <p>
    Use it. The "free tier" in our stack is a recommendation, not a
    rule. Cursor Pro is genuinely good. The point is that you don't
    <em>need</em> it to start. If you have it, use it.
  </p>

  <h3>Do I need a fancy computer?</h3>
  <p>
    No. A Raspberry Pi 4, an old laptop, a $5/mo VPS — all fine. Hermes
    runs on anything that runs Python. The LLMs run in the cloud
    (OpenRouter), not on your machine. If you want to run local models
    too, you'd want a Mac with Apple Silicon or a GPU box, but it's
    optional.
  </p>

  <h3>What's the catch with "free"?</h3>
  <p>
    Most "free" tiers have limits: rate limits, soft pauses, storage
    caps. None of them will block you from learning and shipping a
    small project. When you hit a limit, you'll know exactly what
    you're paying for. That's the right time to spend money.
  </p>

  <hr>

  <h2>🚀 Getting started</h2>

  <h3>I'm a complete beginner. Where do I start?</h3>
  <p>
    <a href="{{ '/start/' | relative_url }}">Start Here</a>. It walks you
    through the whole setup in an hour. Don't skip steps. Don't read
    ahead. Just do it.
  </p>

  <h3>I'm a senior engineer. Do I really need to read the syllabus?</h3>
  <p>
    Probably not. Skim <a href="{{ '/tools/' | relative_url }}">Tools & Pricing</a>
    and <a href="{{ '/hermes/' | relative_url }}">Hermes Agent</a>.
    Pick a <a href="{{ '/projects/' | relative_url }}">project</a> and ship it.
  </p>

  <h3>I'm a founder / indie hacker. What's the shortest path to a shipped product?</h3>
  <p>
    Skip Module 0 (you have a stack). Do Module 1 (prompting). Pick
    Project 5 (ask-my-repo) or Project 6 (HN digest). Build it in
    a weekend. Iterate. Ship.
  </p>

  <h3>Can I skip Hermes and just use Claude Code?</h3>
  <p>
    Yes. You'll miss cron and multi-channel, but for 80% of vibe coding
    work, Claude Code alone is fine. Add Hermes when you need
    scheduled jobs, multi-agent, or 24/7 automation.
  </p>

  <hr>

  <h2>💬 Community</h2>

  <h3>Is there a Discord?</h3>
  <p>
    Use the <a href="https://github.com/{{ site.github_username }}/{{ site.github_repo }}/discussions" target="_blank" rel="noopener">GitHub Discussions</a>
    for now. We don't run a Discord server (yet). If someone wants to
    spin one up, PR welcome.
  </p>

  <h3>Can I teach this to others?</h3>
  <p>
    Yes. MIT-licensed. Take the syllabus, the project ideas, even
    the CSS. Just don't claim you built it. Link back.
  </p>

  <h3>How do I get help if I'm stuck?</h3>
  <ol>
    <li>Read the relevant module page (start, syllabus, hermes, tools)</li>
    <li>Search the <a href="https://github.com/{{ site.github_username }}/{{ site.github_repo }}/discussions" target="_blank" rel="noopener">Discussions</a></li>
    <li>Open a Discussion if your question is new</li>
    <li>Open an Issue if something is actually broken</li>
  </ol>

  <h3>How do I report a typo / broken link?</h3>
  <p>
    PR or issue on the <a href="https://github.com/{{ site.github_username }}/{{ site.github_repo }}" target="_blank" rel="noopener">GitHub repo</a>.
    We love typo fixes.
  </p>

  <hr>

  <div class="callout">
    <span class="icon-c">❓</span>
    <p>
      <strong>Still have a question?</strong> Open a
      <a href="https://github.com/{{ site.github_username }}/{{ site.github_repo }}/discussions" target="_blank" rel="noopener">Discussion</a>
      on the repo. We read all of them.
    </p>
  </div>

</div>
