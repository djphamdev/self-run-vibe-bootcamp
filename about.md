---
layout: default
title: "About"
description: "Why we built this. The camp costs money. We don't. Same skills, free stack."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Why this exists</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">About</h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      A free, public-spirited reverse-engineering of a paid bootcamp.
      Built by one impatient builder who didn't want to wait until October.
    </p>
  </div>
</div>

<div class="container" style="max-width: 760px; padding-bottom: 60px;">

  <h2>The short version</h2>
  <p>
      On July 1st, 2026, I found a syllabus for the <strong>LA TechWeek Vibe
      Coding Camp</strong> — an in-person, <a href="https://luma.com/s0qgwh1y" target="_blank" rel="noopener">registration-required</a>, all-day event on
      October 15, 2026 in Los Angeles. The content looked great. The setup
      also assumed I'd pay for Cursor, ZeroDB, AIKit, and use their
      "experimental" OpenClaw for multi-agent stuff.
    </p>
  <p>
    I'm impatient. I'm budget-oriented. And I don't like being gatekept.
    So I reverse-engineered the syllabus, kept the lessons, swapped the
    tools for free ones, replaced OpenClaw with <strong>Hermes Agent</strong>
    (which does the same job but is production-ready), and put it all
    online for anyone who wants to learn this stuff <em>now</em>.
  </p>

  <h2>The longer version</h2>
  <p>
    I'm a builder. I've been shipping small projects on the open web for
    a while — AI agents, content scrapers, dataset businesses, personal
    wikis. My setup is: a Pi in my closet, Hermes Agent running on it,
    OpenRouter for models, GitHub Pages for hosting, Cloudflare for
    domains, Convex for backends when I need them. The whole thing costs
    me ~$15/year.
  </p>
  <p>
    When I saw the Vibe Coding Camp syllabus, I had two reactions:
    <strong>1)</strong> "this is exactly the kind of thing I would have
    wanted as a beginner", and <strong>2)</strong> "I don't need to pay
    for any of this, I already have a free stack that does all of it."
  </p>
  <p>
    So I figured — let me just put my stack side-by-side with theirs,
    point people at the free alternatives, and let them self-direct.
    That's literally this site.
  </p>

  <h2>What's free is in good faith</h2>
  <p>
    I'm not calling out the camp organizers to be a jerk. AINative Studio
    is doing real work. The original syllabus is a real curriculum. They
    just happen to monetize it via tool fees. I monetize nothing here.
    No email capture. No affiliate links. No "upgrade to Pro." Just docs
    and a syllabus.
  </p>
  <p>
    If you can pay for Cursor Pro and ZeroDB, you'll have a great time
    at the actual camp. If you can't (or don't want to), you'll have a
    great time here instead. Same skills, different invoice.
  </p>

  <h2>What this is <em>not</em></h2>
  <ul>
    <li><strong>Not affiliated with AINative Studio.</strong> This is a fan project.</li>
    <li><strong>Not a paid course.</strong> Free forever, MIT-licensed.</li>
    <li><strong>Not certification.</strong> No certificate, no badge, no resume line.</li>
    <li><strong>Not a replacement for actual building.</strong> Read, then ship.</li>
  </ul>

  <h2>What this <em>is</em></h2>
  <ul>
    <li>A reverse-engineered syllabus, free</li>
    <li>A free stack comparison, with my picks and why</li>
    <li>A working Hermes Agent tutorial</li>
    <li>A set of project ideas you can clone and ship</li>
    <li>A community of builders figuring it out together</li>
  </ul>

  <h2>How to use this site</h2>
  <ol>
    <li>Read <a href="{{ '/start/' | relative_url }}">Start Here</a> — 5 min</li>
    <li>Skim <a href="{{ '/syllabus/' | relative_url }}">Syllabus</a> — 15 min</li>
    <li>Install the free stack — 1 hour</li>
    <li>Pick a <a href="{{ '/projects/' | relative_url }}">Project</a> and build it</li>
    <li>Share what you ship on GitHub, link back here</li>
  </ol>

  <h2>Contributing</h2>
  <p>
    This is open source. PRs welcome for:
  </p>
  <ul>
    <li>New free tools to add to the comparison</li>
    <li>Better exercises in the syllabus</li>
    <li>Project write-ups (in <code>/projects/community/</code>)</li>
    <li>Hermes skills that others can use</li>
    <li>Fixing my typos (there are many)</li>
  </ul>
  <p>
    See the <a href="https://github.com/{{ site.github_username }}/{{ site.github_repo }}" target="_blank" rel="noopener">GitHub repo</a> for contribution guidelines.
  </p>

  <h2>License</h2>
  <p>MIT. Take it, fork it, ship it, don't blame me if something breaks.</p>

  <hr>

  <div class="callout">
    <span class="icon-c">∅</span>
    <p>
      <strong>— Don</strong><br>
      Builder. Sysadmin. Tinkerer. Running Hermes on a Pi in the closet.<br>
      <a href="https://github.com/djphamdev" target="_blank" rel="noopener">github.com/djphamdev</a>
    </p>
  </div>

</div>
