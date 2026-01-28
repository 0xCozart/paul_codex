# PAUL Framework

**Plan-Apply-Unify Loop** — A structured AI-assisted development framework for Claude Code.

![Terminal](assets/terminal.svg)

## Philosophy

PAUL is **not another task runner**. It's a loop-first development framework that ensures every unit of work completes properly.

| Principle | Description |
|-----------|-------------|
| **Loop Integrity** | Every plan closes with UNIFY — never skip |
| **Acceptance-Driven** | Define acceptance criteria before tasks |
| **Minimal Surface** | 13 commands max, not 26 |
| **Composable** | Core loop + optional extensions |
| **One Context** | One loop at a time, no parallel complexity |

## Installation

```bash
npx paul-framework --global
```

Or install locally to a project:

```bash
npx paul-framework --local
```

## The Loop

Every unit of work follows this cycle:

```
┌─────────────────────────────────────┐
│  PLAN ──▶ APPLY ──▶ UNIFY          │
│                                     │
│  Define    Execute    Reconcile     │
│  work      tasks      & close       │
└─────────────────────────────────────┘
```

**Never skip UNIFY.** Every plan needs a summary.

## Quick Start

```bash
# 1. Initialize PAUL in your project
/paul:init

# 2. Create a plan
/paul:plan

# 3. Execute the plan (after approval)
/paul:apply .paul/phases/01-xxx/01-01-PLAN.md

# 4. Close the loop
/paul:unify .paul/phases/01-xxx/01-01-PLAN.md

# 5. Check your progress
/paul:status
```

## Commands

Run `/paul:help` for the complete command reference.

**Core Loop:**
- `/paul:init` — Initialize PAUL in a project
- `/paul:plan` — Create an executable plan
- `/paul:apply` — Execute an approved plan
- `/paul:unify` — Reconcile and close the loop
- `/paul:status` — Show current loop position
- `/paul:help` — Show command reference

## Project Structure

```
.paul/
├── PROJECT.md     # Project context
├── ROADMAP.md     # Phase breakdown
├── STATE.md       # Loop position & state
└── phases/
    └── 01-xxx/
        ├── 01-01-PLAN.md
        └── 01-01-SUMMARY.md
```

## Why PAUL?

**vs. ad-hoc AI coding:** PAUL adds structure without bureaucracy. You get traceability and quality gates while maintaining velocity.

**vs. GSD:** PAUL is simpler (6 core commands vs 26), focuses on loop integrity, and uses acceptance-driven development. GSD is feature-rich; PAUL is focused.

**vs. traditional planning:** PAUL is designed for AI-assisted development. Plans are executable prompts, not documentation.

## Roadmap

See [ROADMAP.md](.paul/ROADMAP.md) for the version plan.

- **v0.1** — Core Loop (current)
- **v0.2** — Session Continuity
- **v0.3** — Roadmap Management
- **v0.4** — Pre-Planning
- **v1.0** — Production Release

## License

MIT

## Author

Chris Kahler — [Chris AI Systems](https://github.com/chriskahler)
