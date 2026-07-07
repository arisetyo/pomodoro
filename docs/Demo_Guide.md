# Demo Guide — AI-Enabled Pomodoro Development

This guide walks you through a complete demo of AI-enabled software development with token optimization, using the Pomodoro web-app as the example project.

---

## Prerequisites

Before starting the demo, install the following tools and dependencies.

### CLI Tools

| Tool | Purpose | Install |
|------|---------|---------|
| [`tree`](https://formulae.brew.sh/formula/tree) | Directory visualization | `brew install tree` |
| [`rtk`](https://github.com/rtk-ai/rtk) | Token-optimized command output | See repo README |
| [`Graphify`](https://github.com/safishamsi/graphify) | AST knowledge graph generation | See repo README |
| [`ast-grep`](https://github.com/ast-grep/ast-grep) | Structural source code search | See repo README |

### VS Code Extension

Build and install the **AI Engineering Coach** extension from source:

- Repo: https://github.com/microsoft/AI-Engineering-Coach

This extension provides a dashboard to monitor your AI-assisted development progress throughout the demo.

### SDD Framework

This demo uses [OpenSpec](https://openspec.dev/) as the Spec-Driven Development (SDD) framework. Install it following the instructions on the site.

### Python Tooling

The project itself is a Python web app, so you need:

- [`uv`](https://docs.astral.sh/uv/) — fast Python package and project manager
- `venv` — included with Python 3.3+

Set up the project environment:

```bash
uv venv
source .venv/bin/activate
```

---

## Demo Steps

### Step 1 — Review `AGENTS.md`

Open [`AGENTS.md`](../AGENTS.md) in the repository root.

This file contains the instructions related to **token optimization** and project conventions. Walk through:

- The project overview and tech stack (FastAPI, htmx, Alpine.js, CSS)
- The **RTK (Rust Token Killer)** section — explains how prefixing commands with `rtk` reduces token usage by 60–90% across builds, tests, git, and more
- The **Graphify** protocol — how to use `graph.json` for codebase context before reading source files
- The **ast-grep** preference over `grep` for source code searches

> 💡 Talking point: AGENTS.md is the single source of truth that AI agents read to understand how to work efficiently in this repo.

---

### Step 2 — Show baseline token savings with `rtk gain`

Run the following in the terminal:

```bash
rtk gain
```

This displays your current **token savings statistics** from using RTK-prefixed commands. Take note of the baseline numbers — you'll compare against this again in Steps 6 and 7.

```bash
rtk gain --history
```

Use `--history` to show a per-command breakdown of savings across recent sessions.

---

### Step 3 — Open the AI Engineering Coach dashboard

Open the **AI Engineering Coach** extension in VS Code (look for its icon in the sidebar or command palette).

Review:

- Current development status and metrics
- Any active recommendations or coaching tips
- Token usage and efficiency indicators

This is your **baseline snapshot**. You'll return to the dashboard at the end of the demo to compare progress.

---

### Step 4 — Use OpenSpec to complete the project

This is the core of the demo: driving development through the OpenSpec SDD workflow.

#### 4.a — Explore the domain

Run the OpenSpec explore command:

```
/opsx:explore
```

In the discussion, tell the agent about the domain reference document:

- [`/docs/Pomodoro_Technique.md`](./Pomodoro_Technique.md)

This document explains the Pomodoro Technique — the six steps, the role of breaks, and the planning/tracking phases. Use it as the source of truth for the feature requirements.

> 💡 Goal: understand the domain before writing any specs or code.

#### 4.b — Propose the MVP

Run:

```
/opsx:propose create-mvp
```

Create a proposal named **`create-mvp`**. This proposal should cover the minimal viable Pomodoro app:

- A 25-minute focus timer
- A short break (5–10 minutes)
- A long break (20–30 minutes) after four pomodori
- Start / pause / reset controls
- Simple session counter (no persistence)

OpenSpec will generate the design, specs, and task list for the change.

#### 4.c — Apply the change

Run:

```
/opsx:apply
```

This implements the tasks defined in the `create-mvp` proposal. The agent will:

1. Read the delta specs
2. Generate or modify the FastAPI routes, htmx templates, Alpine.js components, and CSS
3. Mark tasks complete as it progresses

Verify the app runs:

```bash
source .venv/bin/activate
uv run uvicorn app.main:app --reload
```

Open the displayed local URL and try the timer.

#### 4.d — Archive the change

Once the MVP is complete and verified, run:

```
/opsx:archive
```

This finalizes the `create-mvp` change, syncs the delta specs into the main specs, and moves the change into the archive under `openspec/changes/archive/`.

---

### Step 5 — Scan the repo with Graphify

Now that the codebase exists, generate a knowledge graph for future development and navigation.

#### 5.a — Generate and show `graph.json`

Make sure `.graphifyignore` exists, then run:

```bash
graphify .
```

This creates `graphify-out/graph.json`. Open it and show:

- The **god nodes** (high-centrality modules)
- The **community detection** clusters
- The dependency edges between modules

> 💡 Talking point: this graph lets future AI sessions locate symbols without scanning the whole repo — a major token saver.

#### 5.b — Create and show `graph.html`

Generate an interactive HTML visualization:

```bash
graphify cluster-only .
```

Open the resulting HTML file in a browser and walk through the cluster view of the codebase architecture.

#### 5.c — Create and show the callflow HTML

Generate a call-flow report from `graph.json`:

```bash
uvx --from graphifyy graphify export callflow-html
```

Open the generated callflow HTML and demonstrate how to trace a request path through the FastAPI routes → htmx templates → Alpine.js handlers.

---

### Step 6 — Check `rtk gain` again

Run:

```bash
rtk gain
```

Compare the new savings numbers against the baseline from **Step 2**. You should see a noticeable increase from all the `rtk`-prefixed commands run during the demo (builds, tests, git operations, etc.).

```bash
rtk gain --history
```

Highlight which command categories contributed the most savings.

---

### Step 7 — Check the AI Engineering Coach dashboard again

Reopen the **AI Engineering Coach** dashboard in VS Code.

Compare against the baseline from **Step 3**:

- Progress on tasks completed
- Token efficiency metrics
- Any new coaching recommendations

> 💡 Wrap-up: the dashboard should reflect the work completed through the OpenSpec workflow and the token savings captured by RTK throughout the session.

---

## Summary

| Step | Action | Tool |
|------|--------|------|
| 1 | Review token-optimization instructions | `AGENTS.md` |
| 2 | Baseline token savings | `rtk gain` |
| 3 | Baseline dev status | AI Engineering Coach |
| 4 | Build the MVP via SDD | OpenSpec |
| 5 | Generate codebase knowledge graph | Graphify |
| 6 | Final token savings | `rtk gain` |
| 7 | Final dev status | AI Engineering Coach |

By the end of this demo, you will have:

- ✅ Built a working Pomodoro web app using a spec-driven workflow
- ✅ Generated a navigable knowledge graph of the codebase
- ✅ Measured concrete token savings from RTK
- ✅ Tracked your AI-assisted development progress end-to-end
