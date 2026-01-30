---
name: paul:discuss
description: Explore and articulate phase vision before planning
argument-hint: "<phase-number>"
allowed-tools: [Read, Write, AskUserQuestion]
---

<objective>
Facilitate vision discussion for a specific phase and create context handoff.

**When to use:** Before planning a phase, when goals and approach need exploration.
</objective>

<execution_context>
@~/.claude/paul-framework/workflows/discuss-phase.md
</execution_context>

<context>
Phase number: $ARGUMENTS (required)

@.paul/PROJECT.md
@.paul/STATE.md
@.paul/ROADMAP.md
</context>

<process>
Follow workflow: @~/.claude/paul-framework/workflows/discuss-phase.md
</process>

<success_criteria>
- [ ] CONTEXT.md created in phase directory
- [ ] Goals and approach articulated
- [ ] Ready for /paul:plan command
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/discuss.md` (generalized discussion command)

### Adapted from GSD
- Thin wrapper pattern (command delegates to workflow)
- YAML frontmatter structure
- @-reference pattern (execution_context for static, context for dynamic)
- Workflow delegation via `Follow workflow:` instruction

### PAUL Adaptations
- **Phase-focused:** Specialized for phase vision discussions (vs milestone-level)
- **Requires argument:** Takes phase number to target specific phase
- **Context handoff:** Creates CONTEXT.md in phase directory for planning
- **Distinct from /paul:assumptions:** discuss is user input, assumptions is Claude analysis
