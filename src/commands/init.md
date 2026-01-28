---
name: paul:init
description: Initialize PAUL in a project
argument-hint:
allowed-tools: [Read, Write, Bash, Glob, AskUserQuestion]
---

<objective>
Initialize the `.paul/` structure in a project directory.

**When to use:** Starting a new project with PAUL, or adding PAUL to an existing codebase.

Creates PROJECT.md, STATE.md, and ROADMAP.md with initial structure.
</objective>

<execution_context>
@src/workflows/init-project.md
@src/templates/PROJECT.md
@src/templates/STATE.md
@src/templates/ROADMAP.md
</execution_context>

<context>
Current directory state (check for existing .paul/)
</context>

<process>
Follow workflow: @src/workflows/init-project.md
</process>

<success_criteria>
- [ ] .paul/ directory created
- [ ] PROJECT.md initialized with project context
- [ ] STATE.md initialized with loop position
- [ ] ROADMAP.md initialized with phase structure
</success_criteria>

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `commands/gsd/new-project.md`

### Adapted from GSD
- Thin wrapper pattern (command delegates to workflow)
- YAML frontmatter structure (name, description, argument-hint, allowed-tools)
- Section order (objective, execution_context, context, process, success_criteria)
- @-reference separation (execution_context vs context)

### PAUL Adaptations
- **Simpler scope:** No mode/depth/parallelization config prompts (PAUL handles at workflow level)
- **No brownfield detection:** Codebase mapping is a separate concern, not embedded in init
- **Directory structure:** Creates `.paul/` instead of `.planning/`
- **Fewer questions:** Init is lightweight; deep questioning happens in plan-phase if needed
- **No git init:** Assumes project already has git (or doesn't require it)
