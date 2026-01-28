<purpose>
Reconcile what was planned vs. what was built. Create SUMMARY.md documenting results, update STATE.md with new position, and close the loop to prepare for next PLAN.
</purpose>

<when_to_use>
- APPLY phase complete (all tasks executed or documented)
- Ready to close the current loop
- Need to record what was built for future reference
</when_to_use>

<loop_context>
Expected phase: UNIFY
Prior phase: APPLY (execution complete)
Next phase: PLAN (next plan or next phase)
</loop_context>

<required_reading>
@.paul/STATE.md
@.paul/phases/{phase}/{plan}-PLAN.md
</required_reading>

<references>
@~/.claude/paul-framework/references/loop-phases.md
@~/.claude/paul-framework/templates/SUMMARY.md
</references>

<process>

<step name="gather_results" priority="first">
1. Recall execution from APPLY phase:
   - Which tasks completed successfully
   - Which tasks failed (if any)
   - Which checkpoints were resolved and how
   - Any deviations from the plan
2. Read PLAN.md to refresh:
   - Original acceptance criteria
   - Expected outputs
   - Task definitions
</step>

<step name="compare_plan_vs_actual">
1. For each acceptance criterion:
   - Was it satisfied? (PASS/FAIL)
   - Evidence of satisfaction
2. For each task:
   - Did it complete as specified?
   - Any modifications to approach?
3. Note deviations:
   - What differed from plan
   - Why it differed
   - Impact on outcomes
</step>

<step name="create_summary">
1. Create SUMMARY.md at `.paul/phases/{phase}/{plan}-SUMMARY.md`
2. Include:

   **Frontmatter:**
   ```yaml
   ---
   phase: NN-name
   plan: NN
   completed: ISO timestamp
   duration: approximate time
   ---
   ```

   **Sections:**
   - Objective (brief restatement)
   - What Was Built (table: file, purpose, lines)
   - Acceptance Criteria Results (table: AC, description, status)
   - Verification Results (command outputs)
   - Deviations (if any, with explanations)
   - Key Patterns/Decisions (if any emerged)
   - Next Phase (what comes next)
</step>

<step name="update_state">
1. Update STATE.md:

   **Current Position:**
   - Phase: N of M - Complete (or In Progress if more plans)
   - Plan: complete
   - Status: Ready for next PLAN
   - Last activity: timestamp

   **Progress:**
   - Update milestone percentage
   - Update phase percentage (100% if complete)

   **Loop Position:**
   ```
   PLAN ──▶ APPLY ──▶ UNIFY
     ✓        ✓        ✓     [Loop complete - ready for next PLAN]
   ```

   **Session Continuity:**
   - Update stopped at
   - Update next action
   - Update resume file (point to SUMMARY)
</step>

<step name="update_roadmap">
If this completes the phase (all plans done):

1. Read ROADMAP.md
2. Update phase table:
   - Status: Complete
   - Completed: date
3. Update "Phases: X of Y complete"
4. Mark plan checkbox: `[x]`
</step>

<step name="signal_completion">
Report with quick continuation prompt:
```
════════════════════════════════════════
LOOP COMPLETE
════════════════════════════════════════

Plan: {NN}-{plan} — [description]
[summary of what was built]
[deviations if any]

---
Continue to next PLAN?

[1] Yes, plan next | [2] Pause here
```

**Accept quick inputs:** "1", "yes", "continue", "go" → run `/paul:plan` for next phase/plan
</step>

</process>

<output>
- SUMMARY.md at `.paul/phases/{phase}/{plan}-SUMMARY.md`
- Updated STATE.md
- Updated ROADMAP.md (if phase complete)
</output>

<error_handling>
**APPLY not complete:**
- Check STATE.md for actual position
- If APPLY incomplete, cannot UNIFY
- Return to APPLY to complete or document blockers

**Missing execution context:**
- If no memory of execution results, read any logs
- Ask user to confirm what was completed
- Document uncertainty in SUMMARY.md

**PLAN.md missing:**
- Cannot reconcile without original plan
- Ask user to locate or reconstruct
</error_handling>

<anti_patterns>
**Skipping SUMMARY:**
Every completed plan MUST have a SUMMARY.md. No exceptions.

**Partial state updates:**
Update ALL of: SUMMARY, STATE, ROADMAP (if phase done). Don't leave partial.

**Vague summaries:**
"It worked" is not a summary. Document files, AC results, deviations specifically.

**Forgetting loop position:**
Always show the visual loop position in STATE.md.
</anti_patterns>
