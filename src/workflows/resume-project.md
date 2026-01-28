<purpose>
Resume PAUL work after a session break. Reads STATE.md to restore context, determines current loop position, and guides continuation of work.
</purpose>

<when_to_use>
- Starting a new session on an existing PAUL project
- Context was cleared (new conversation)
- Handoff from another session
- User asks to "continue" or "resume" PAUL work
</when_to_use>

<loop_context>
Determined dynamically by reading STATE.md.
This workflow figures out where we are, not assumes it.
</loop_context>

<required_reading>
@.paul/STATE.md
</required_reading>

<references>
@src/references/context-management.md
@src/references/loop-phases.md
</references>

<process>

<step name="verify_paul_exists" priority="first">
1. Check for .paul/ directory:
   ```bash
   ls .paul/STATE.md 2>/dev/null
   ```
2. If not found:
   - "No PAUL project found. Run init-project first."
   - Offer to initialize
3. If found: proceed with resume
</step>

<step name="load_state">
1. Read `.paul/STATE.md`
2. Extract:
   - Current Position (phase, plan, status)
   - Loop Position (PLAN/APPLY/UNIFY markers)
   - Last activity (what was happening)
   - Session Continuity section:
     - Stopped at
     - Next action
     - Resume file
     - Resume context
</step>

<step name="load_resume_context">
1. If resume file specified in STATE.md:
   - Read the resume file (PLAN, SUMMARY, or HANDOFF)
2. If handoff file exists:
   - Check for recent HANDOFF-*.md files
   - Load if more recent than STATE.md
3. Build mental picture of:
   - What was accomplished
   - What's in progress
   - What's next
</step>

<step name="determine_action">
Based on loop position:

**If PLAN ○ (no plan yet):**
- Next action: Create PLAN.md for current phase
- "Ready to create Plan [NN]-01. Starting plan-phase workflow."

**If PLAN ✓, APPLY ○ (plan exists, not executed):**
- Read the PLAN.md
- "Plan exists at [path]. Awaiting approval to execute."
- Present plan summary
- Wait for approval

**If PLAN ✓, APPLY ✓, UNIFY ○ (executed, not reconciled):**
- "APPLY complete but loop not closed. Running UNIFY."
- Trigger unify-phase workflow

**If all ✓ (loop complete):**
- "Previous loop complete. Ready for next PLAN."
- Check if more plans in phase or next phase
- Trigger plan-phase workflow
</step>

<step name="report_position">
Display to user:

```
════════════════════════════════════════
PAUL PROJECT RESUMED
════════════════════════════════════════

Project: [from PROJECT.md]
Phase: [N] of [M] - [Phase Name]
Plan: [NN]-[plan] or "None yet"

Loop Position:
PLAN ──▶ APPLY ──▶ UNIFY
  [✓/○]   [✓/○]   [✓/○]

Last Activity: [timestamp] - [description]

Next Action: [what to do]
════════════════════════════════════════
```
</step>

<step name="offer_options">
Present options to user:

1. **Continue** - Proceed with determined next action
2. **Review state** - Show full STATE.md
3. **Review plan** - Show current/recent PLAN.md
4. **Adjust** - Override determined action

Wait for user direction before proceeding.
</step>

</process>

<output>
- Context restored
- User informed of current position
- Ready to continue appropriate workflow
</output>

<error_handling>
**STATE.md corrupted or incomplete:**
- Report what's missing
- Offer to reconstruct from ROADMAP + phases/

**Conflicting information:**
- STATE.md says X, but files suggest Y
- Report discrepancy
- Ask user to clarify actual state

**No resume context:**
- If SESSION CONTINUITY section empty:
- Fall back to loop position
- Ask user what they remember

**Stale handoff:**
- If handoff older than STATE.md modifications
- Trust STATE.md, note handoff may be outdated
</error_handling>

<bootstrap_without_commands>
When commands don't exist yet (pre-Phase 5), this workflow
provides the entry point for PAUL methodology.

**Manual bootstrap sequence:**
1. Read this workflow's process
2. Execute steps manually
3. Based on determined action, read appropriate workflow:
   - Need PLAN? → plan-phase.md
   - Need APPLY? → apply-phase.md
   - Need UNIFY? → unify-phase.md

This section will be deprecated once /paul:resume command exists.
</bootstrap_without_commands>
