# Project: Pomodoro web-app using Python

## About

This project is a web-based Pomodoro app created using Python.
Simple session with no data persistence.
This project is only for demo, not production.

## Tech stack

- FastAPI (web service)
- htmx (backend interactivity)
- Alpine.js (UI/X interactivity)
- CSS (styling)

Use `rtk tree` to check the repo structure.

## Architecture

- This is a monolithic web application using Python as the web service
- Interaction between server and frontend uses htmx
- Animation and other UX elements in the frontend use Alpine.js
- No local storage or database is needed

## Operations

**Prompt:**
Always ensure that any Python command is run inside an activated virtual environment (`.venv`).
Before running a Python command, activate the virtual environment using:

```bash
source .venv/bin/activate
```

Use `uv` to run installations, tests, and other Python commands to ensure they are executed within the virtual environment.

For example, to install a package, use:
```bash
uv pip install <package-name>
```


---


## Context Retrieval Policy

Always retrieve the smallest amount of information necessary.
Escalate only when necessary. Stop escalating as soon as sufficient information has been obtained.

Preferred order:
1. Need code structure? `graph.json`.
2. Need symbols? `ast-grep`.
3. Need repository metadata? `rtk`.
4. Need implementation? Source files.
5. Use repository-wide search as last resort

Avoid reading entire directories or the whole repository unless explicitly requested.


<!-- rtk-instructions v2 -->
## RTK (Rust Token Killer) - Token-Optimized Commands

### Golden Rule

**Always prefix commands with `rtk`**. If RTK has a dedicated filter, it uses it. If not, it passes through unchanged. This means RTK is always safe to use.

**Important**: Even in command chains with `&&`, use `rtk`:
```bash
# ❌ Wrong
git add . && git commit -m "msg" && git push

# ✅ Correct
rtk git add . && rtk git commit -m "msg" && rtk git push
```

### RTK Commands by Workflow

#### Build & Compile (80-90% savings)
```bash
rtk cargo build         # Cargo build output
rtk cargo check         # Cargo check output
rtk cargo clippy        # Clippy warnings grouped by file (80%)
rtk tsc                 # TypeScript errors grouped by file/code (83%)
rtk lint                # ESLint/Biome violations grouped (84%)
rtk prettier --check    # Files needing format only (70%)
rtk next build          # Next.js build with route metrics (87%)
```

#### Test (60-99% savings)
```bash
rtk cargo test          # Cargo test failures only (90%)
rtk go test             # Go test failures only (90%)
rtk jest                # Jest failures only (99.5%)
rtk vitest              # Vitest failures only (99.5%)
rtk playwright test     # Playwright failures only (94%)
rtk pytest              # Python test failures only (90%)
rtk rake test           # Ruby test failures only (90%)
rtk rspec               # RSpec test failures only (60%)
rtk test <cmd>          # Generic test wrapper - failures only
```

#### Git (59-80% savings)
```bash
rtk git status          # Compact status
rtk git log             # Compact log (works with all git flags)
rtk git diff            # Compact diff (80%)
rtk git show            # Compact show (80%)
rtk git add             # Ultra-compact confirmations (59%)
rtk git commit          # Ultra-compact confirmations (59%)
rtk git push            # Ultra-compact confirmations
rtk git pull            # Ultra-compact confirmations
rtk git branch          # Compact branch list
rtk git fetch           # Compact fetch
rtk git stash           # Compact stash
rtk git worktree        # Compact worktree
```

Note: Git passthrough works for ALL subcommands, even those not explicitly listed.

#### GitHub (26-87% savings)
```bash
rtk gh pr view <num>    # Compact PR view (87%)
rtk gh pr checks        # Compact PR checks (79%)
rtk gh run list         # Compact workflow runs (82%)
rtk gh issue list       # Compact issue list (80%)
rtk gh api              # Compact API responses (26%)
```

#### JavaScript/TypeScript Tooling (70-90% savings)
```bash
rtk pnpm list           # Compact dependency tree (70%)
rtk pnpm outdated       # Compact outdated packages (80%)
rtk pnpm install        # Compact install output (90%)
rtk npx <cmd>           # Compact npx command output
rtk prisma              # Prisma without ASCII art (88%)
```

#### Files & Search (60-75% savings)
```bash
rtk ls <path>           # Tree format, compact (65%)
rtk read <file>         # Code reading with filtering (60%)
rtk grep <pattern>      # Search grouped by file (75%). Format flags (-c, -l, -L, -o, -Z) run raw.
rtk find <pattern>      # Find grouped by directory (70%)
```

#### Analysis & Debug (70-90% savings)
```bash
rtk err <cmd>           # Filter errors only from any command
rtk log <file>          # Deduplicated logs with counts
rtk json <file>         # JSON structure without values
rtk deps                # Dependency overview
rtk env                 # Environment variables compact
rtk summary <cmd>       # Smart summary of command output
rtk diff                # Ultra-compact diffs
```

#### Infrastructure (85% savings)
```bash
rtk docker ps           # Compact container list
rtk docker images       # Compact image list
rtk docker logs <c>     # Deduplicated logs
rtk kubectl get         # Compact resource list
rtk kubectl logs        # Deduplicated pod logs
```

#### Network (65-70% savings)
```bash
rtk curl <url>          # Compact HTTP responses (70%)
rtk wget <url>          # Compact download output (65%)
```

#### Meta Commands
```bash
rtk gain                # View token savings statistics
rtk gain --history      # View command history with savings
rtk discover            # Analyze Claude Code sessions for missed RTK usage
rtk proxy <cmd>         # Run command without filtering (for debugging)
rtk init                # Add RTK instructions to CLAUDE.md
rtk init --global       # Add RTK to ~/.claude/CLAUDE.md
```

### Token Savings Overview

| Category | Commands | Typical Savings |
|----------|----------|-----------------|
| Tests | vitest, playwright, cargo test | 90-99% |
| Build | next, tsc, lint, prettier | 70-87% |
| Git | status, log, diff, add, commit | 59-80% |
| GitHub | gh pr, gh run, gh issue | 26-87% |
| Package Managers | pnpm, npm, npx | 70-90% |
| Files | ls, read, grep, find | 60-75% |
| Infrastructure | docker, kubectl | 85% |
| Network | curl, wget | 65-70% |

Overall average: **60-90% token reduction** on common development operations.
<!-- /rtk-instructions -->


## Graphify - Codebase context & knowledge graph protocol

A pre-computed AST knowledge graph (`graph.json`) is available at: `graphify-out/graph.json`
Use `graph.json` before searching or reading multiple source files.

Workflow:
1. Read `graph.json`.
2. Identify the relevant symbols, files, and dependency paths.
3. Read only the source files required for the task.
4. Avoid scanning unrelated files.

Use the graph for:
- dependency tracing
- call-path discovery
- identifying high-centrality modules
- impact analysis before refactoring
- locating symbol definitions

Never read an entire directory simply to locate a symbol. Use `graph.json` to locate the symbol first, then read only the relevant files.

The graph is generated from AST extraction and represents extracted structural relationships only. Treat graph edges as authoritative for structural relationships.
Do not infer dependencies that are absent from the graph.


## ast-grep

Prefer `ast-grep` over `grep` whenever searching source code.

Use `ast-grep` for:
- locating function definitions
- locating class definitions
- locating method implementations
- finding imports
- matching AST patterns
- performing structural search

Use `grep` only for:
- Markdown
- JSON
- YAML
- log files
- generated text
- plain-text configuration

Avoid using `grep` to search programming language source code when `ast-grep` can answer the query.