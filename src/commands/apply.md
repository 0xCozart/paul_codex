---
name: paul:apply
description: Execute an approved PLAN
argument-hint: "[plan-path]"
allowed-tools: [Read, Write, Edit, Bash, Glob, Grep, AskUserQuestion]
---

<objective>
Execute an approved PLAN.md file, handling checkpoints as they occur.

**When to use:** After PLAN phase complete and plan is approved.

Executes tasks in sequence, pauses at checkpoints for user input, reports completion.
</objective>

<execution_context>
@src/workflows/apply-phase.md
@src/references/checkpoints.md
</execution_context>

<context>
Plan path: $ARGUMENTS

@.paul/STATE.md
</context>

<process>

<step name="validate_plan">
1. Confirm plan file exists at $ARGUMENTS path
2. Error if not found: "Plan not found: {path}"
3. Derive SUMMARY path (replace PLAN.md with SUMMARY.md)
4. If SUMMARY exists: "Plan already executed. SUMMARY: {path}"
   - Offer: re-execute or exit
</step>

<step name="execute">
Follow workflow: @src/workflows/apply-phase.md

Execute tasks sequentially. For each task:
- Read task definition
- Execute action
- Run verification
- Confirm done criteria
</step>

<step name="handle_checkpoints">
When a checkpoint task is reached:

**checkpoint:decision**
- Present decision context and options
- Wait for user selection
- Record decision
- Continue execution

**checkpoint:human-verify**
- Present what was built
- Present verification steps
- Wait for "approved" or issue description
- If issues: address and re-verify
- Continue execution

**checkpoint:human-action**
- Present required action
- Wait for "done" confirmation
- Continue execution
</step>

<step name="complete">
After all tasks complete:
- Report: "APPLY complete. Run /paul:unify to close loop."
- Show files modified
- Show SUMMARY path to create
</step>

</process>

<success_criteria>
- [ ] All tasks executed
- [ ] All checkpoints handled
- [ ] User informed of completion
- [ ] Next action clear (run /paul:unify)
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/execute-plan.md`

### Adapted from GSD
- Plan validation pattern (check exists, check not already executed)
- SUMMARY path derivation from PLAN path
- Checkpoint handling types (decision, human-verify, human-action)
- Checkpoint presentation format (context, options, resume signal)
- Completion reporting with next steps

### PAUL Adaptations
- **No subagent spawning:** GSD spawns subagent for execution; PAUL executes in current context
- **Simpler checkpoint handling:** No agent resume mechanism; just pause/continue in conversation
- **Directory structure:** References `.paul/` instead of `.planning/`
- **Workflow delegation:** Delegates to apply-phase.md instead of embedding execution logic
- **Explicit next step:** Directs to /paul:unify (GSD doesn't have equivalent)
