---
name: paul:status
description: Show current PAUL loop position and progress
argument-hint:
allowed-tools: [Read]
---

<objective>
Display current loop position (PLAN/APPLY/UNIFY) and phase progress.

**When to use:** Check where you are in the PAUL loop, see what's next.
</objective>

<execution_context>
</execution_context>

<context>
@.paul/STATE.md
@.paul/ROADMAP.md
</context>

<process>

<step name="read_state">
Read STATE.md and extract:
- Current milestone
- Current phase (X of Y)
- Current plan status
- Loop position (PLAN/APPLY/UNIFY)
- Last activity
</step>

<step name="display_status">
Display formatted status:

```
PAUL Status
════════════════════════════════════════

Milestone: [name]
Phase: [X of Y] ([phase name])
Plan: [status]

Loop Position:
┌─────────────────────────────────────┐
│  PLAN ──▶ APPLY ──▶ UNIFY          │
│   [✓/○]    [✓/○]    [✓/○]          │
└─────────────────────────────────────┘

Last: [timestamp] — [activity]
Next: [recommended action]

════════════════════════════════════════
```
</step>

<step name="suggest_next">
Based on loop position, suggest next action:
- If PLAN needed: "Run /paul:plan to create plan"
- If PLAN ready: "Approve plan, then run /paul:apply"
- If APPLY complete: "Run /paul:unify to close loop"
- If UNIFY complete: "Loop closed. Ready for next phase."
</step>

</process>

<success_criteria>
- [ ] Loop position displayed clearly
- [ ] Phase progress shown
- [ ] Next action suggested
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/status.md`

### Adapted from GSD
- Status display concept
- Reading project state files
- Formatted output with box drawing

### PAUL Innovations (Significant Departure)
- **Loop-focused:** PAUL status shows PLAN/APPLY/UNIFY position, not background agents
- **Much simpler:** Read-only operation, no TaskOutput polling or agent tracking
- **Visual loop diagram:** Displays the characteristic PAUL loop with checkmarks
- **No parallel agent tracking:** GSD tracks spawned agents; PAUL focuses on loop state
- **Prescriptive next action:** Tells user exactly what command to run next

This command is a PAUL innovation. GSD's status monitors parallel execution agents. PAUL's status shows where you are in the Plan-Apply-Unify loop and what to do next.
