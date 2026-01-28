---
paths:
  - "src/commands/**/*.md"
---

# Command Rules

Rules for editing files in `src/commands/`.

## File Structure

```yaml
---
name: paul:command-name
description: One-line description
argument-hint: "<required>" or "[optional]"
allowed-tools: [Read, Write, Bash, Glob, Grep, Edit, AskUserQuestion]
---
```

## Section Order

1. `<objective>` — What/why/when (always present)
2. `<execution_context>` — @-references to workflows, templates, references
3. `<context>` — Dynamic content: `$ARGUMENTS`, bash output, @file refs
4. `<process>` or `<step>` elements — Implementation steps (thin, delegates to workflow)
5. `<success_criteria>` — Measurable completion checklist

## Core Principle

**Commands are thin wrappers.** Delegate detailed logic to workflows.

Commands answer "what to do", workflows answer "how to do it".

A command should fit on one screen. If it grows beyond that, logic belongs in a workflow.

## @-Reference Patterns

```markdown
<execution_context>
@src/workflows/plan-phase.md
@src/templates/PLAN.md
@src/references/checkpoints.md
</execution_context>

<context>
$ARGUMENTS

@.paul/PROJECT.md
@.paul/STATE.md
@.paul/ROADMAP.md
</context>
```

- `execution_context`: Static resources (workflows, templates, references from PAUL framework)
- `context`: Dynamic project state (from `.paul/` directory) and user arguments

## Success Criteria Format

```xml
<success_criteria>
- [ ] Specific, measurable criterion
- [ ] Another verifiable outcome
</success_criteria>
```

Use checkbox format. Each criterion must be objectively verifiable.

## Example Command Structure

```markdown
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
```

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `~/.claude/get-shit-done/.claude/rules/commands.md`

### Adapted from GSD
- YAML frontmatter structure (name, description, argument-hint, allowed-tools)
- Section order (objective, execution_context, context, process, success_criteria)
- Core principle: Commands are thin wrappers
- @-reference separation (execution_context vs context)
- Success criteria checkbox format

### PAUL Adaptations
- **Command prefix:** `paul:` instead of `gsd:`
- **Path pattern:** `src/commands/` instead of `commands/gsd/`
- **Project state:** References `.paul/` instead of `.planning/`
- **Allowed tools:** Added `Edit` to default tool list
- **Example:** Provided complete paul:plan example structure
- **CARL integration:** Commands work alongside CARL domains (noted but not enforced in rules)
