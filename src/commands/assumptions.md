---
name: paul:assumptions
description: Surface Claude's assumptions about a phase before planning
argument-hint: "<phase-number>"
allowed-tools: [Read, Bash]
---

<objective>
Surface Claude's assumptions about a phase to validate understanding before planning.

**When to use:** Before planning to catch misconceptions early.

**Distinction from /paul:discuss:** This command shows what CLAUDE thinks. The discuss command gathers what USER wants.
</objective>

<execution_context>
@~/.claude/paul-framework/workflows/phase-assumptions.md
</execution_context>

<context>
Phase number: $ARGUMENTS (required)

@.paul/PROJECT.md
@.paul/STATE.md
@.paul/ROADMAP.md
</context>

<process>
Follow workflow: @~/.claude/paul-framework/workflows/phase-assumptions.md
</process>

<success_criteria>
- [ ] Assumptions presented across 5 areas
- [ ] Confidence levels indicated
- [ ] User can provide corrections
- [ ] Clear path to planning after validation
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/list-phase-assumptions.md`

### Adapted from GSD
- Thin wrapper pattern (command delegates to workflow)
- YAML frontmatter structure
- Phase number argument
- @-reference pattern (execution_context for static, context for dynamic)
- Workflow delegation via `Follow workflow:` instruction

### PAUL Adaptations
- **Shorter name:** `assumptions` instead of `list-phase-assumptions`
- **Explicit distinction:** Documented difference from discuss command
- **Workflow reuse:** Routes to existing phase-assumptions.md workflow
