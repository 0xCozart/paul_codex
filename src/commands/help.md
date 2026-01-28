---
name: paul:help
description: Show available PAUL commands and usage guide
---

<objective>
Display the complete PAUL command reference.

Output ONLY the reference content below. Do NOT add:

- Project-specific analysis
- Git status or file context
- Next-step suggestions
- Any commentary beyond the reference
</objective>

<reference>
# PAUL Command Reference

**PAUL** (Plan-Apply-Unify Loop) is a structured AI-assisted development framework for Claude Code.

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

1. `/paul:init` - Initialize PAUL in your project
2. `/paul:plan` - Create a plan for your work
3. `/paul:apply <plan-path>` - Execute the approved plan
4. `/paul:unify <plan-path>` - Close the loop with summary

## Commands

### Core Loop

### `/paul:init`
Initialize PAUL in a project.

- Creates `.paul/` directory structure
- Creates PROJECT.md, STATE.md, ROADMAP.md
- Sets up phase directories

Usage: `/paul:init`

---

### `/paul:plan [phase]`
Enter PLAN phase - create an executable plan.

- Reads current state from STATE.md
- Creates PLAN.md with tasks, acceptance criteria, boundaries
- Updates loop position

Usage: `/paul:plan` (auto-detects next phase)
Usage: `/paul:plan 3` (specific phase)

---

### `/paul:apply <plan-path>`
Execute an approved PLAN.md file.

- Validates plan exists and hasn't been executed
- Executes tasks sequentially
- Handles checkpoints (decision, human-verify, human-action)
- Reports completion

Usage: `/paul:apply .paul/phases/01-foundation/01-01-PLAN.md`

---

### `/paul:unify <plan-path>`
Reconcile plan vs actual and close the loop.

- Creates SUMMARY.md documenting what was built
- Records decisions made, deferred issues
- Updates STATE.md with loop closure
- **Required** - never skip this step

Usage: `/paul:unify .paul/phases/01-foundation/01-01-PLAN.md`

---

### `/paul:status` *(deprecated)*
> Use `/paul:progress` instead.

Shows current loop position. Deprecated in favor of `/paul:progress` which provides better routing.

Usage: `/paul:status`

---

### Session Continuity (v0.2)

### `/paul:pause [reason]`
Create handoff file and prepare for session break.

- Creates HANDOFF.md with complete context
- Updates STATE.md session continuity section
- Designed for context limits or multi-session work

Usage: `/paul:pause`
Usage: `/paul:pause "switching to other project"`

---

### `/paul:resume`
Restore context from handoff and continue work.

- Reads STATE.md and any HANDOFF files
- Determines current loop position
- Suggests exact next action

Usage: `/paul:resume`

---

### `/paul:progress [context]`
Smart status with routing - suggests ONE next action.

- Shows milestone and phase progress visually
- Displays current loop position
- Suggests exactly ONE next action (prevents decision fatigue)
- Accepts optional context to tailor suggestion
- Warns about context limits

Usage: `/paul:progress`
Usage: `/paul:progress "I only have 30 minutes"`

---

### Utility

### `/paul:help`
Show this command reference.

Usage: `/paul:help`

## Files & Structure

```
.paul/
├── PROJECT.md           # Project context and value prop
├── ROADMAP.md           # Phase breakdown and timeline
├── STATE.md             # Loop position and session state
└── phases/
    ├── 01-foundation/
    │   ├── 01-01-PLAN.md
    │   └── 01-01-SUMMARY.md
    └── 02-features/
        ├── 02-01-PLAN.md
        └── 02-01-SUMMARY.md
```

## PLAN.md Structure

```markdown
---
phase: 01-foundation
plan: 01
type: execute
autonomous: true
---

<objective>
Goal, Purpose, Output
</objective>

<acceptance_criteria>
Given/When/Then format
</acceptance_criteria>

<tasks>
<task type="auto">...</task>
</tasks>

<boundaries>
DO NOT CHANGE, SCOPE LIMITS
</boundaries>

<verification>
Completion checks
</verification>
```

## Task Types

| Type | Use For |
|------|---------|
| `auto` | Fully autonomous execution |
| `checkpoint:decision` | Choices requiring human input |
| `checkpoint:human-verify` | Visual/functional verification |
| `checkpoint:human-action` | Manual steps (rare) |

## Common Workflows

**Starting a new project:**
```
/paul:init
/paul:plan 1
# Approve plan
/paul:apply .paul/phases/01-foundation/01-01-PLAN.md
/paul:unify .paul/phases/01-foundation/01-01-PLAN.md
```

**Checking where you are:**
```
/paul:progress   # State + ONE next action (recommended)
```

**Resuming work (new session):**
```
/paul:resume     # Restores context, suggests next action
```

**Pausing work (before break):**
```
/paul:pause      # Creates handoff, updates state
```

## Key Principles

1. **Loop must complete** - PLAN → APPLY → UNIFY, no shortcuts
2. **Commands are thin** - Logic lives in workflows
3. **State is tracked** - STATE.md knows where you are
4. **Boundaries are real** - Respect DO NOT CHANGE sections
5. **Acceptance criteria first** - Define done before starting

## Getting Help

- Run `/paul:progress` to see where you are and what to do next
- Read `.paul/PROJECT.md` for project context
- Read `.paul/STATE.md` for current position
- Check `.paul/ROADMAP.md` for phase overview
</reference>
