<purpose>
Initialize PAUL structure in a new project. Creates .paul/ directory with PROJECT.md, ROADMAP.md, STATE.md, and phases/ directory - everything needed to start using PAUL methodology.
</purpose>

<when_to_use>
- Starting PAUL in a project that doesn't have .paul/ directory
- User explicitly requests project initialization
- Beginning a new project from scratch
</when_to_use>

<loop_context>
N/A - This is a setup workflow, not a loop phase.
After init, project is ready for first PLAN.
</loop_context>

<process>

<step name="check_existing" priority="first">
1. Check if .paul/ directory exists:
   ```bash
   ls .paul/ 2>/dev/null
   ```
2. If exists:
   - Warn: "PAUL already initialized in this project"
   - Offer options:
     a) Resume existing (use resume-project workflow)
     b) Reset (delete and reinitialize - destructive)
     c) Cancel
3. If not exists: proceed with initialization
</step>

<step name="gather_project_info">
1. Determine project context:
   - Project name (from directory or user input)
   - Brief description (what it does)
   - Core value proposition (why it matters)
2. Identify initial phases:
   - Ask user OR infer from project type
   - Typical starting phases: Foundation, Core Features, Polish
3. Get any known requirements or constraints
</step>

<step name="create_structure">
1. Create directories:
   ```bash
   mkdir -p .paul/phases
   ```
2. Confirm structure created
</step>

<step name="create_project_md">
Create `.paul/PROJECT.md`:

```markdown
# Project: [Name]

## Description
[Brief description of what this project does]

## Core Value
[Why this project matters - the key value proposition]

## Requirements

### Must Have
- [Essential requirement 1]
- [Essential requirement 2]

### Should Have
- [Important but not critical]

### Nice to Have
- [Optional enhancements]

## Constraints
- [Technical constraints]
- [Time/resource constraints]

## Success Criteria
- [How we know the project succeeded]

---
*Created: [timestamp]*
```
</step>

<step name="create_roadmap_md">
Create `.paul/ROADMAP.md`:

```markdown
# Roadmap: [Project Name]

## Overview
[Brief description of project journey]

## Current Milestone
**v0.1 [Milestone Name]** (v0.1.0)
Status: Not started
Phases: 0 of N complete

## Phases

| Phase | Name | Plans | Status | Completed |
|-------|------|-------|--------|-----------|
| 1 | [Phase 1 Name] | TBD | Not started | - |
| 2 | [Phase 2 Name] | TBD | Not started | - |
| 3 | [Phase 3 Name] | TBD | Not started | - |

## Phase Details

### Phase 1: [Name]
**Goal:** [What this phase accomplishes]
**Depends on:** Nothing (first phase)

**Scope:**
- [Deliverable 1]
- [Deliverable 2]

**Plans:**
- [ ] 01-01: [Plan description]

[Repeat for other phases]

---
*Roadmap created: [timestamp]*
```
</step>

<step name="create_state_md">
Create `.paul/STATE.md`:

```markdown
# Project State

## Project Reference
See: .paul/PROJECT.md

**Core value:** [From PROJECT.md]
**Current focus:** v0.1 [Milestone] — Phase 1

## Current Position
Milestone: v0.1 [Name]
Phase: 1 of N ([Phase Name]) — Not started
Plan: None yet
Status: Ready to create first PLAN
Last activity: [timestamp] — Project initialized

Progress:
- Milestone: [░░░░░░░░░░] 0%
- Phase 1: [░░░░░░░░░░] 0%

## Loop Position

Current loop state:
```
PLAN ──▶ APPLY ──▶ UNIFY
  ○        ○        ○     [Ready for first PLAN]
```

## Accumulated Context

### Decisions
None yet.

### Deferred Issues
None yet.

### Blockers/Concerns
None yet.

## Session Continuity
Last session: [timestamp]
Stopped at: Project initialization
Next action: Create Phase 1 PLAN.md
Resume file: .paul/ROADMAP.md

---
*STATE.md — Updated after every significant action*
```
</step>

<step name="report_completion">
Report to user:

1. Structure created:
   ```
   .paul/
   ├── PROJECT.md
   ├── ROADMAP.md
   ├── STATE.md
   └── phases/
   ```

2. Next step: "Run paul:plan to create your first PLAN, or manually create a PLAN.md following the template."

3. Suggest reviewing:
   - PROJECT.md for accuracy
   - ROADMAP.md for phase structure
</step>

</process>

<output>
- `.paul/` directory structure
- `.paul/PROJECT.md`
- `.paul/ROADMAP.md`
- `.paul/STATE.md`
- `.paul/phases/` (empty directory)
</output>

<error_handling>
**Permission denied:**
- Report filesystem error
- Ask user to check permissions

**Invalid project info:**
- Use sensible defaults
- Mark as "[TBD]" for user to fill in

**Partial creation failure:**
- Report what was created vs failed
- Offer to retry or clean up
</error_handling>
