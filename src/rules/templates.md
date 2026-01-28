---
paths:
  - "src/templates/**/*.md"
---

# Template Rules

Rules for editing files in `src/templates/`.

## File Structure

Templates define the structure for generated documents. Each template file contains:

1. **Header** — `# [NAME].md Template`
2. **Intro** — Brief description and file naming pattern
3. **File Template block** — The actual template in a fenced code block
4. **Field documentation** — Tables explaining frontmatter fields, sections
5. **Examples/Anti-patterns** — Good vs bad usage
6. **GSD Parity Documentation** — Source references and adaptations (REQUIRED)

## Placeholder Conventions

**Square brackets** for human-fillable placeholders:
```
[Project Name]
[Description of what this accomplishes]
[Specific implementation instructions]
```

**Curly braces** for variable interpolation:
```
{phase}-{plan}-PLAN.md
.paul/phases/{phase-number}-{name}/
```

## YAML Frontmatter in Template Content

Templates that define output documents show example frontmatter:

```yaml
---
phase: XX-name
plan: NN
type: execute
wave: 1
depends_on: []
files_modified: []
autonomous: true
---
```

This is content TO BE GENERATED, not frontmatter for the template file itself.

## GSD Parity Documentation Requirement

**Every template MUST include a GSD Parity Documentation section.**

This section has three parts:

```markdown
## GSD Parity Documentation

### Source Reference
- **GSD File:** `~/.claude/get-shit-done/templates/[equivalent].md`
- **GSD Workflow:** `~/.claude/get-shit-done/workflows/[related].md` (if applicable)

### Adapted from GSD
- [Pattern 1 from GSD]
- [Pattern 2 from GSD]

### PAUL Innovations Beyond GSD
- **[Innovation name]:** [Description of what PAUL adds]
```

This documents provenance and ensures deliberate adaptation.

## Template Quality Checklist

Before completing a template:

- [ ] Clear naming pattern documented
- [ ] All fields have purpose documented in a table
- [ ] Examples show correct usage
- [ ] Anti-patterns show what to avoid (with WHY)
- [ ] GSD Parity Documentation section present
- [ ] Template renders valid markdown when filled

## Key Principle

Templates show structure for generated documents. They are reference material for workflows and humans creating PAUL artifacts.

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `~/.claude/get-shit-done/.claude/rules/templates.md`

### Adapted from GSD
- Placeholder conventions (square brackets vs curly braces)
- YAML frontmatter clarification (content to be generated, not template metadata)
- Key principle: Templates show structure for generated documents

### PAUL Adaptations
- **File structure:** Defined explicit section order (header, intro, template, fields, examples, parity docs)
- **GSD Parity requirement:** PAUL mandates parity documentation in every template (GSD doesn't require this)
- **Quality checklist:** Added pre-completion checklist for template authors
- **Path pattern:** `src/templates/` instead of `get-shit-done/templates/`
