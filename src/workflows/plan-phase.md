<purpose>
Create an executable PLAN.md for the current or specified phase. The plan defines objective, acceptance criteria, tasks, boundaries, and verification - everything needed for APPLY phase execution.
</purpose>

<when_to_use>
- Starting a new phase (ROADMAP shows next phase ready)
- Previous plan completed (loop closed with UNIFY)
- First plan in a project (after init-project)
- Resuming work that needs a new plan
</when_to_use>

<loop_context>
Expected phase: PLAN
Prior phase: UNIFY (previous plan complete) or none (first plan)
Next phase: APPLY (after plan approval)
</loop_context>

<required_reading>
@.paul/STATE.md
@.paul/ROADMAP.md
@.paul/PROJECT.md
@.paul/phases/{prior-phase}/{plan}-SUMMARY.md (if exists and relevant)
</required_reading>

<references>
@src/references/plan-format.md
@src/references/checkpoints.md (if plan will have checkpoints)
@src/templates/PLAN.md
</references>

<process>

<step name="validate_preconditions" priority="first">
1. Read STATE.md to confirm:
   - Loop position is ready for PLAN (prior UNIFY complete or first plan)
   - No blockers preventing planning
2. If STATE.md shows mid-loop (APPLY or UNIFY incomplete):
   - Warn user: "Previous loop not closed. Complete UNIFY first or reset."
   - Do not proceed until resolved
</step>

<step name="identify_phase">
1. Read ROADMAP.md to determine:
   - Which phase is next (first incomplete phase)
   - Phase scope and goals
   - Dependencies on prior phases
2. If multiple phases available, ask user which to plan
3. Confirm phase selection before proceeding
</step>

<step name="analyze_scope">
1. Review phase goals from ROADMAP.md
2. Estimate number of tasks needed:
   - Target: 2-3 tasks per plan
   - If >3 tasks, consider splitting into multiple plans
3. Identify files that will be modified
4. Determine if checkpoints are needed:
   - Visual verification required? → checkpoint:human-verify
   - Architecture decision needed? → checkpoint:decision
   - Unavoidable manual action? → checkpoint:human-action (rare)
5. Set autonomous flag: true if no checkpoints, false otherwise
</step>

<step name="load_context">
1. Read PROJECT.md for:
   - Core requirements and constraints
   - Value proposition (what matters)
2. If prior phase exists, read its SUMMARY.md for:
   - What was built
   - Decisions made
   - Any deferred issues
3. Read source files relevant to this phase's work
4. Do NOT reflexively chain all prior summaries - only load what's genuinely needed
</step>

<step name="create_plan">
1. Create phase directory: `.paul/phases/{NN}-{phase-name}/`
2. Generate PLAN.md following template structure:

   **Frontmatter:**
   - phase: NN-name
   - plan: 01 (or next number if multiple plans in phase)
   - type: execute (or tdd/research)
   - wave: 1 (adjust if dependencies exist)
   - depends_on: [] (or prior plan IDs if genuine dependency)
   - files_modified: [list all files]
   - autonomous: true/false

   **Sections:**
   - <objective>: Goal, Purpose, Output
   - <context>: @-references to project files and source
   - <acceptance_criteria>: Given/When/Then for each criterion
   - <tasks>: Task definitions with files, action, verify, done
   - <boundaries>: DO NOT CHANGE, SCOPE LIMITS
   - <verification>: Overall completion checks
   - <success_criteria>: Measurable completion
   - <output>: SUMMARY.md location

3. Ensure every task has:
   - Clear files list
   - Specific action (not vague)
   - Verification command/check
   - Done criteria linking to AC-N
</step>

<step name="validate_plan">
1. Check all sections present
2. Verify acceptance criteria are testable
3. Confirm tasks are specific enough (files + action + verify + done)
4. Ensure boundaries protect completed work
5. Validate checkpoint placement (if any):
   - After automated work completes
   - Before dependent decisions
   - Not too frequent (avoid checkpoint fatigue)
</step>

<step name="update_state">
1. Update STATE.md:
   - Current Position: Phase X, Plan Y created
   - Loop Position: PLAN ✓ → APPLY ○ → UNIFY ○
   - Last activity: timestamp and action
   - Session Continuity: point to new PLAN.md
2. Report to user:
   - "Plan created at: [path]"
   - "Ready for approval. Execute when you approve."
</step>

</process>

<output>
PLAN.md at `.paul/phases/{NN}-{phase-name}/{NN}-{plan}-PLAN.md`

Example: `.paul/phases/04-workflows-layer/04-01-PLAN.md`
</output>

<error_handling>
**STATE.md missing:**
- Offer to create from ROADMAP.md inference
- Or ask user to run init-project first

**ROADMAP.md missing:**
- Cannot plan without roadmap
- Ask user to create ROADMAP.md or run init-project

**Phase dependencies not met:**
- Warn user which prior phases must complete first
- Do not create plan until dependencies satisfied
</error_handling>
