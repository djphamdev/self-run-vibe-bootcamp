---
layout: default
title: "Module 4: UI Components"
description: "Ship beautiful front-ends without designing. shadcn/ui, daisyUI, Mamba UI, Radix — all free, copy-paste."
---

<div class="container" style="padding: 60px 24px 40px;">
  <div style="max-width: 760px; margin: 0 auto;">
    <div class="hero-badge" style="margin-bottom: 20px;">
      <span class="dot"></span>
      <span>Module 4 · ~2 hrs · Copy-paste UI</span>
    </div>
    <h1 style="font-size: clamp(36px, 5vw, 56px); margin-bottom: 20px;">
      UI <span class="accent">Components</span>
    </h1>
    <p class="lede" style="font-size: 18px; color: var(--text-2); margin-bottom: 32px;">
      The camp uses AIKit ($$). We use free libraries you own. Copy → paste → customize.
    </p>
  </div>
</div>

<div class="container" style="max-width: 900px; padding-bottom: 60px;">

  <div class="callout">
    <span class="icon-c">🎯</span>
    <p><strong>Goal:</strong> A working dark-mode UI with: landing page, dashboard layout, data table, modal, toast notifications. Zero design decisions.</p>
  </div>

  <h2>🆚 Free component libraries</h2>
  <table class="compare">
    <thead>
      <tr><th>Library</th><th>Approach</th><th>Best for</th><th>Learning curve</th></tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>shadcn/ui</strong></td>
        <td>Copy-paste components into your repo. You own the code.</td>
        <td>React/Next.js, full control, customization</td>
        <td>Low (if you know React)</td>
      </tr>
      <tr>
        <td><strong>daisyUI</strong></td>
        <td>Tailwind plugin. Class names like <code>btn btn-primary</code>.</td>
        <td>Speed, semantic classes, themes</td>
        <td>Very low</td>
      </tr>
      <tr>
        <td><strong>Mamba UI</strong></td>
        <td>Tailwind components. Free, no attribution.</td>
        <td>Landing pages, marketing sites</td>
        <td>Low</td>
      </tr>
      <tr>
        <td><strong>Radix Primitives</strong></td>
        <td>Unstyled, accessible primitives. Build your own look.</td>
        <td>Design systems, total control</td>
        <td>Medium</td>
      </tr>
      <tr>
        <td><strong>Headless UI</strong></td>
        <td>Unstyled, React/Vue. From Tailwind team.</td>
        <td>Custom components, accessibility</td>
        <td>Medium</td>
      </tr>
    </tbody>
  </table>

  <h2>⚡ Fastest path: daisyUI + vanilla HTML</h2>
  <p>No build step. Works in any static site (Jekyll, Astro, plain HTML).</p>

  <h3>1. Add to <code><head></code></h3>
  <div class="prompt"><script src="https://cdn.tailwindcss.com"></script>
<link href="https://cdn.jsdelivr.net/npm/daisyui@4.12.10/dist/full.min.css" rel="stylesheet" type="text/css" />
<script>tailwind.config = { darkMode: "class" }</script></div>

  <h3>2. Landing page in 50 lines</h3>
  <details class="code-block">
    <summary>landing.html</summary>
    <pre><code><!DOCTYPE html>
<html class="h-full="h-full" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My AI App</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/daisyui@4.12.10/dist/full.min.css" rel="stylesheet">
  <script>tailwind.config = { darkMode: "class" }</script>
</head>
<body class="min-h-screen bg-base-200">
  <!-- NAVBAR -->
  <div class="navbar bg-base-100 shadow-sm">
    <div class="navbar-start">
      <a class="btn btn-ghost text-xl font-bold">∅ MyApp</a>
    </div>
    <div class="navbar-center hidden lg:flex">
      <a class="btn btn-ghost" href="#features">Features</a>
      <a class="btn btn-ghost" href="#pricing">Pricing</a>
      <a class="btn btn-ghost" href="#docs">Docs</a>
    </div>
    <div class="navbar-end">
      <a class="btn btn-primary" href="/app">Launch App</a>
    </div>
  </div>

  <!-- HERO -->
  <section class="hero min-h-[60vh]">
    <div class="hero-content text-center">
      <div class="max-w-2xl">
        <h1 class="text-5xl font-bold">Build with AI.<br><span class="text-primary">Ship today.</span></h1>
        <p class="py-6 text-base-content/70">Your AI-native app, running on free infrastructure. No credit card. No gatekeeping.</p>
        <div class="flex justify-center gap-4">
          <a class="btn btn-primary btn-lg" href="/app">Start Free</a>
          <a class="btn btn-outline btn-lg" href="/docs">Read Docs</a>
        </div>
      </div>
    </div>
  </section>

  <!-- FEATURES -->
  <section id="features" class="py-20 px-4">
    <div class="max-w-5xl mx-auto">
      <h2 class="text-3xl font-bold text-center mb-12">Why developers choose us</h2>
      <div class="grid md:grid-cols-3 gap-6">
        <div class="card bg-base-100 shadow-xl">
          <div class="card-body">
            <div class="text-4xl mb-4">🤖</div>
            <h3 class="card-title">AI-Native</h3>
            <p>Built for LLMs from day one. Vector search, agents, RAG — all included.</p>
          </div>
        </div>
        <div class="card bg-base-100 shadow-xl">
          <div class="card-body">
            <div class="text-4xl mb-4">💰</div>
            <h3 class="card-title">Free Forever</h3>
            <p>OpenRouter free tier, GitHub Pages, Cloudflare. $0 to start, ~$5/mo at scale.</p>
          </div>
        </div>
        <div class="card bg-base-100 shadow-xl">
          <div class="card-body">
            <div class="text-4xl mb-4">🔓</div>
            <h3 class="card-title">You Own It</h3>
            <p>Your code, your data, your domain. No vendor lock-in. MIT licensed.</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer bg-base-100 p-10">
    <div class="max-w-5xl mx-auto grid md:grid-cols-3 gap-8">
      <div>
        <h3 class="font-bold text-lg mb-4">∅ MyApp</h3>
        <p class="text-base-content/70">Self-run vibe coding. Ship AI apps for money, not just skills.</p>
      </div>
      <div>
        <h3 class="font-bold text-lg mb-4">Links</h3>
        <ul class="space-y-2">
          <li><a class="text-base-content/70 hover:text-primary" href="#">GitHub</a></li>
          <li><a class="text-base-content/70 hover:text-primary" href="#">Discord</a></li>
          <li><a class="text-base-content/70 hover:text-primary" href="#">Docs</a></li>
        </ul>
      </div>
      <div>
        <h3 class="font-bold text-lg mb-4">Legal</h3>
        <ul class="space-y-2">
          <li><a class="text-base-content/70 hover:text-primary" href="#">Privacy</a></li>
          <li><a class="text-base-content/70 hover:text-primary" href="#">Terms</a></li>
        </ul>
      </div>
    </div>
    <div class="divider"></div>
    <p class="text-center text-base-content/50 text-sm">MIT Licensed · Built with <span class="text-primary">∅</span></p>
  </footer>
</body>
</html>
</code></pre>
  </details>

  <h2>🔧 shadcn/ui (React/Next.js) — for the app</h2>
  <p>When you need a real dashboard, not a landing page.</p>

  <h3>Setup (30 seconds)</h3>
  <div class="prompt">npx shadcn@latest init
# Answer: TypeScript, Slate, CSS variables, ~

npx shadcn@latest add button card dialog table toast tabs sidebar
# Adds: components/ui/*.tsx + lib/utils.ts</div>

  <h3>Dashboard layout (copy-paste)</h3>
  <details class="code-block">
    <summary>app/dashboard/layout.tsx</summary>
    <pre><code>"use client";
import { Sidebar, SidebarHeader, SidebarContent, SidebarGroup, SidebarMenu, SidebarMenuItem, SidebarMenuButton } from "@/components/ui/sidebar";
import { Button } from "@/components/ui/button";
import { Home, Settings, Database, Bot, LogOut } from "lucide-react";

export function DashboardSidebar() {
  return (
    <Sidebar>
      <SidebarHeader>
        <h2 class="px-4 py-2 font-bold text-lg">∅ MyApp</h2>
      </SidebarHeader>
      <SidebarContent>
        <SidebarGroup>
          <SidebarMenu>
            <SidebarMenuItem><SidebarMenuButton asChild><a href="/dashboard"><Home class="mr-2 h-4 w-4" />Overview</a></SidebarMenuButton></SidebarMenuItem>
            <SidebarMenuItem><SidebarMenuButton asChild><a href="/dashboard/agents"><Bot class="mr-2 h-4 w-4" />Agents</a></SidebarMenuButton></SidebarMenuItem>
            <SidebarMenuItem><SidebarMenuButton asChild><a href="/dashboard/memory"><Database class="mr-2 h-4 w-4" />Memory</a></SidebarMenuButton></SidebarMenuItem>
            <SidebarMenuItem><SidebarMenuButton asChild><a href="/dashboard/settings"><Settings class="mr-2 h-4 w-4" />Settings</a></SidebarMenuButton></SidebarMenuItem>
          </SidebarMenu>
        </SidebarGroup>
        <SidebarGroup>
          <SidebarMenu>
            <SidebarMenuItem><SidebarMenuButton asChild><a href="/logout"><LogOut class="mr-2 h-4 w-4" />Sign Out</a></SidebarMenuButton></SidebarMenuItem>
          </SidebarMenu>
        </SidebarGroup>
      </SidebarContent>
    </Sidebar>
  );
}
</code></pre>
  </details>

  <h3>Data table with actions</h3>
  <details class="code-block">
    <summary>components/agent-table.tsx</summary>
    <pre><code>"use client";
import { ColumnDef } from "@tanstack/react-table";
import { DataTable } from "@/components/ui/data-table";
import { Button } from "@/components/ui/button";
import { Edit, Trash2, Play } from "lucide-react";

export const agentColumns: ColumnDef<Agent>[] = [
  { accessorKey: "name", header: "Agent", cell: ({ row }) => <span class="font-mono">{row.getValue("name")}</span> },
  { accessorKey: "status", header: "Status", cell: ({ row }) => (
    <span class={`badge ${row.getValue("status") === "running" ? "badge-success" : "badge-ghost"}`}>
      {row.getValue("status")}
    </span>
  )},
  { accessorKey: "schedule", header: "Schedule", cell: ({ row }) => <span class="font-mono text-sm">{row.getValue("schedule")}</span> },
  { accessorKey: "lastRun", header: "Last Run", cell: ({ row }) => new Date(row.getValue("lastRun")).toLocaleString() },
  {
    id: "actions",
    header: "",
    cell: ({ row }) => (
      <div class="flex items-center gap-2">
        <Button variant="ghost" size="icon"><Play class="h-4 w-4" /></Button>
        <Button variant="ghost" size="icon"><Edit class="h-4 w-4" /></Button>
        <Button variant="ghost" size="icon" class="text-red-500"><Trash2 class="h-4 w-4" /></Button>
      </div>
    ),
  },
];
</code></pre>
  </details>

  <h2>✅ Done criteria</h2>
  <ul>
    <li>☐ Landing page deploys to GitHub Pages (static HTML + daisyUI)</li>
    <li>☐ Dashboard loads in Next.js + shadcn/ui (sidebar, table, toast)</li>
    <li>☐ Dark mode works (obviously)</li>
    <li>☐ Responsive: mobile navbar collapses, table scrolls</li>
    <li>☐ (Bonus) Theme switcher: daisyUI <code>data-theme="light|dark|cupcake|cyberpunk"</code></li>
  </ul>

  <h2>🎨 Theming daisyUI (one line)</h2>
  <div class="prompt"><html data-theme="dark">        <!-- or: light, cupcake, bumblebee, emerald, corporate, synthwave, retro, cyberpunk, valentine, halloween, garden, forest, aqua, lofi, pastel, fantasy, wireframe, black, luxury, dracula, cmyk, autumn, business, acid, lemonade, night, coffee, winter, dim, nord, sunset --></div>
  <p>Add a <code><select></code> to let users pick. Persist to <code>localStorage</code>.</p>

  <h2>📚 Resources</h2>
  <ul>
    <li><a href="https://ui.shadcn.com/" target="_blank">shadcn/ui docs</a> — component reference</li>
    <li><a href="https://daisyui.com/" target="_blank">daisyUI docs</a> — components, themes, Tailwind config</li>
    <li><a href="https://mambaui.com/" target="_blank">Mamba UI</a> — free landing page sections</li>
    <li><a href="https://www.radix-ui.com/" target="_blank">Radix Primitives</a> — unstyled accessible components</li>
    <li><a href="https://tailwindcss.com/docs/dark-mode" target="_blank">Tailwind dark mode</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p1">Starter Kit P1: Blog (Jekyll + daisyUI)</a></li>
    <li><a href="{{ '/starter-kits/' | relative_url }}#kit-p5">Starter Kit P5: Ask-My-Repo (Convex + shadcn/ui)</a></li>
  </ul>

  <div class="hero-actions" style="margin-top: 40px;">
    <a href="{{ '/starter-kits/' | relative_url }}" class="btn btn-primary">⚡ Copy a starter kit</a>
    <a href="{{ '/syllabus/' | relative_url }}" class="btn btn-ghost">← Back to syllabus</a>
  </div>

</div>