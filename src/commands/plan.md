---
name: paul:plan
description: Enter PLAN phase for current or new plan
argument-hint: "[phase-plan]"
allowed-tools: [Read, Write, Glob, AskUserQuestion]
---

<objective>
Create or continue a PLAN for the specified phase.

**When to use:** Starting new work or resuming incomplete plan.
</objective>

<execution_context>
@src/workflows/plan-phase.md
@src/templates/PLAN.md
@src/references/plan-format.md
</execution_context>

<context>
$ARGUMENTS

@.paul/PROJECT.md
@.paul/STATE.md
@.paul/ROADMAP.md
</context>

<process>
Follow workflow: @src/workflows/plan-phase.md
</process>

<success_criteria>
- [ ] PLAN.md created in correct phase directory
- [ ] All acceptance criteria defined
- [ ] STATE.md updated with loop position
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/plan-phase.md`

### Adapted from GSD
- Thin wrapper pattern (command delegates to workflow)
- YAML frontmatter structure
- Optional argument for phase specification
- @-reference pattern (execution_context for static, context for dynamic)
- Workflow delegation via `Follow workflow:` instruction

### PAUL Adaptations
- **Directory structure:** References `.paul/` instead of `.planning/`
- **Simpler tools:** No mcp__context7 or WebFetch (PAUL keeps tool set minimal)
- **Template references:** Points to PAUL templates in `src/templates/`
- **Workflow references:** Points to PAUL workflows in `src/workflows/`
