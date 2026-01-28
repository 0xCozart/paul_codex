---
name: paul:unify
description: Reconcile plan vs actual and close the loop
argument-hint: "[plan-path]"
allowed-tools: [Read, Write, AskUserQuestion]
---

<objective>
Reconcile plan versus actual results, create SUMMARY.md, and close the loop.

**When to use:** After APPLY phase complete. This is MANDATORY - never skip UNIFY.

Creates SUMMARY.md documenting what was built, decisions made, and any deferred issues.
</objective>

<execution_context>
@src/workflows/unify-phase.md
@src/templates/SUMMARY.md
</execution_context>

<context>
Plan path: $ARGUMENTS

@.paul/STATE.md
@{plan-path} (the PLAN.md being unified)
</context>

<process>

<step name="validate_preconditions">
1. Confirm PLAN.md exists at $ARGUMENTS path
2. Confirm APPLY phase was executed (tasks completed)
3. If SUMMARY.md already exists: "Loop already closed. SUMMARY: {path}"
</step>

<step name="reconcile">
Follow workflow: @src/workflows/unify-phase.md

Compare plan to actual:
- Which tasks completed as planned?
- Any deviations from plan?
- Decisions made during execution?
- Issues discovered but deferred?
</step>

<step name="create_summary">
Create SUMMARY.md in same directory as PLAN.md:
- Document what was built
- Record acceptance criteria results
- Note any deferred issues
- Capture decisions made
- List files created/modified
</step>

<step name="update_state">
Update STATE.md:
- Loop position: PLAN ✓ → APPLY ✓ → UNIFY ✓
- Phase progress if plan completes phase
- Performance metrics (duration)
- Session continuity (next action)
</step>

<step name="report">
Display:
```
Loop Closed
════════════════════════════════════════

Plan: {plan-path}
Summary: {summary-path}

PLAN ──▶ APPLY ──▶ UNIFY
  ✓        ✓        ✓

Next: [phase complete message or next plan]

════════════════════════════════════════
```
</step>

</process>

<success_criteria>
- [ ] SUMMARY.md created
- [ ] STATE.md updated with loop closure
- [ ] User knows next action
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** None (PAUL innovation)

### PAUL Innovation
This command has no direct GSD equivalent. It represents a core PAUL principle:

**"Never skip UNIFY"** — Every PLAN must have a SUMMARY.

GSD handles reconciliation implicitly within execute-plan subagent returns. PAUL makes it explicit:
- Dedicated command enforces the discipline
- Explicit loop closure visualization
- SUMMARY.md is a first-class artifact, not optional
- STATE.md loop position tracking requires UNIFY to advance

### Why This Matters
The UNIFY phase ensures:
1. Learnings are captured (decisions, deferred issues)
2. Progress is accurately tracked
3. Future sessions have context
4. Incomplete loops are visible in STATE.md

This is the key differentiator in PAUL's "Plan-Apply-Unify" loop versus traditional execute-and-forget patterns.
