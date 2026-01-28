---
name: paul:pause
description: Create handoff file and prepare for session break
argument-hint: [reason]
allowed-tools: [Read, Write, Bash, AskUserQuestion]
---

<objective>
Create a HANDOFF.md file capturing current context and update STATE.md for session continuity.

**When to use:** Before ending a session, switching context, or when context limit is approaching.
</objective>

<execution_context>
@src/workflows/pause-work.md
</execution_context>

<context>
$ARGUMENTS

@.paul/STATE.md
@.paul/PROJECT.md
</context>

<process>
**Follow the pause-work workflow** from `@src/workflows/pause-work.md`.

The workflow handles:
1. Detecting current position
2. Gathering session context (ask user if needed)
3. Creating HANDOFF-{date}.md with populated content
4. Updating STATE.md session continuity
5. Optional WIP commit
6. Confirmation display

If `[reason]` argument provided, include it in handoff status.
</process>

<success_criteria>
- [ ] HANDOFF.md created with complete context (no placeholders)
- [ ] STATE.md updated with session continuity
- [ ] Next action is clear and actionable
- [ ] Resume instructions provided
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/pause-work.md`

### Adapted from GSD
- Handoff creation concept (GSD uses `.continue-here.md`)
- WIP commit pattern
- Session state capture

### PAUL Innovations
- **Workflow delegation:** Command is thin wrapper, logic in workflow
- **Dated handoffs:** `HANDOFF-{date}.md` allows history
- **Centralized location:** Handoffs in `.paul/` root, not phase directories
