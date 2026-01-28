# ROADMAP.md Template

Template for `.paul/ROADMAP.md` — the project's phase structure.

**Purpose:** Define milestones and phases. Provides structure, not detailed tasks.

---

## File Template (Initial v1.0)

```markdown
# Roadmap: [Project Name]

## Overview

[One paragraph describing the journey from start to finish]

## Current Milestone

**[Milestone Name]** ([version])
Status: [Not started | In progress | Complete]
Phases: [X] of [Y] complete

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with [INSERTED])

Phases execute in numeric order: 1 → 2 → 2.1 → 2.2 → 3 → 3.1 → 4

| Phase | Name | Plans | Status | Completed |
|-------|------|-------|--------|-----------|
| 1 | [Name] | [N] | Not started | - |
| 2 | [Name] | [N] | Not started | - |
| 3 | [Name] | [N] | Not started | - |
| 4 | [Name] | [N] | Not started | - |

## Phase Details

### Phase 1: [Name]

**Goal:** [What this phase delivers - specific outcome]
**Depends on:** Nothing (first phase)
**Research:** [Unlikely | Likely] ([reason])

**Scope:**
- [Deliverable 1]
- [Deliverable 2]
- [Deliverable 3]

**Plans:**
- [ ] 01-01: [Brief description]
- [ ] 01-02: [Brief description]
- [ ] 01-03: [Brief description]

### Phase 2: [Name]

**Goal:** [What this phase delivers]
**Depends on:** Phase 1 ([specific dependency])
**Research:** [Unlikely | Likely] ([reason])
**Research topics:** [If Likely - what needs investigating]

**Scope:**
- [Deliverable 1]
- [Deliverable 2]

**Plans:**
- [ ] 02-01: [Brief description]
- [ ] 02-02: [Brief description]

### Phase 2.1: [Name] [INSERTED]

**Goal:** [Urgent work inserted between phases]
**Depends on:** Phase 2
**Reason:** [Why this was inserted]

**Plans:**
- [ ] 02.1-01: [Description]

### Phase 3: [Name]

**Goal:** [What this phase delivers]
**Depends on:** Phase 2 ([specific dependency])
**Research:** [Unlikely | Likely]

**Scope:**
- [Deliverable 1]
- [Deliverable 2]

**Plans:**
- [ ] 03-01: [Brief description]
- [ ] 03-02: [Brief description]

### Phase 4: [Name]

**Goal:** [What this phase delivers]
**Depends on:** Phase 3
**Research:** Unlikely (internal patterns)

**Scope:**
- [Deliverable 1]

**Plans:**
- [ ] 04-01: [Brief description]

---
*Roadmap created: [YYYY-MM-DD]*
*Last updated: [YYYY-MM-DD]*
```

---

## File Template (After v1.0 Ships)

After completing first milestone, reorganize with milestone groupings:

```markdown
# Roadmap: [Project Name]

## Milestones

| Version | Name | Phases | Status | Completed |
|---------|------|--------|--------|-----------|
| v1.0 | MVP | 1-4 | Complete | YYYY-MM-DD |
| v1.1 | [Name] | 5-6 | In progress | - |
| v2.0 | [Name] | 7-10 | Planned | - |

## Active Milestone: v1.1 [Name]

**Goal:** [What v1.1 delivers]
**Status:** Phase [X] of [Y]

### Phase 5: [Name]

**Goal:** [What this phase delivers]
**Depends on:** Phase 4

**Plans:**
- [ ] 05-01: [Brief description]
- [ ] 05-02: [Brief description]

### Phase 6: [Name]

**Goal:** [What this phase delivers]
**Depends on:** Phase 5

**Plans:**
- [ ] 06-01: [Brief description]

## Planned Milestone: v2.0 [Name]

**Goal:** [What v2.0 delivers]
**Prerequisite:** v1.1 complete

[Phase outlines without detailed plans]

## Completed Milestones

<details>
<summary>v1.0 MVP (Phases 1-4) - Shipped YYYY-MM-DD</summary>

### Phase 1: [Name]
**Goal:** [What was delivered]
**Plans:** 3 complete

- [x] 01-01: [Description]
- [x] 01-02: [Description]
- [x] 01-03: [Description]

[... remaining v1.0 phases ...]

</details>

---
*Last updated: [YYYY-MM-DD]*
```

---

## Section Specifications

### Overview
**Purpose:** High-level journey description.
**Length:** One paragraph.
**Update:** When project direction changes significantly.

### Current Milestone
**Purpose:** Quick reference to active milestone.
**Contains:** Name, version, status, phase progress.
**Update:** After each phase completion.

### Phases Table
**Purpose:** At-a-glance view of all phases.
**Contains:** Phase number, name, plan count, status, completion date.
**Update:** After each plan/phase completion.

### Phase Details
**Purpose:** Detailed breakdown of each phase.
**Contains:**
- **Goal:** Specific deliverable outcome
- **Depends on:** Phase dependencies with reason
- **Research:** Likely/Unlikely with justification
- **Scope:** Bullet list of deliverables
- **Plans:** Checklist with brief descriptions

**Update:** During planning; status after completion.

---

## Phase Numbering

**Integer phases (1, 2, 3):** Planned work from roadmap creation.

**Decimal phases (2.1, 2.2):** Urgent insertions.
- Insert between consecutive integers
- Mark with [INSERTED] tag
- Include reason for insertion
- Filesystem sorts correctly: 2 < 2.1 < 2.2 < 3

**Validation for decimal insertion:**
- Integer X must exist and be complete
- Integer X+1 must exist in roadmap
- Decimal X.Y must not already exist
- Y >= 1

---

## Depth Configuration

Phase count depends on project depth:

| Depth | Typical Phases | Plans/Phase |
|-------|----------------|-------------|
| Quick | 3-5 | 1-3 |
| Standard | 5-8 | 3-5 |
| Comprehensive | 8-12 | 5-10 |

**Key principle:** Derive phases from actual work. Depth determines compression tolerance, not a target to hit.

---

## Research Flags

- **Unlikely:** Internal patterns, CRUD operations, established conventions
- **Likely:** External APIs, new libraries, architectural decisions

When `Research: Likely`:
- Include `Research topics:` field
- Consider research phase before implementation
- Discovery may be required during planning

---

## Status Values

| Status | Meaning |
|--------|---------|
| Not started | Phase hasn't begun |
| In progress | Actively working |
| Complete | All plans done (add date) |
| Deferred | Pushed to later (add reason) |

---

## GSD Parity Documentation

### Source Reference
- **GSD File:** `~/.claude/get-shit-done/templates/roadmap.md`

### Adapted from GSD
- Phase numbering (integer + decimal for insertions)
- Phase structure (Goal, Depends on, Research, Plans)
- Research flags (Likely/Unlikely with topics)
- Depth configuration table
- Progress tracking table
- Milestone grouping after v1.0 (collapsed completed milestones)
- Status values (Not started, In progress, Complete, Deferred)
- Plan checklist format

### PAUL Innovations Beyond GSD
- **Current Milestone section** - Quick reference at top for active focus. GSD includes this info but not as prominently.
- **Scope section per phase** - Explicit deliverables list beyond just plans. GSD mentions scope in Goal but doesn't separate.
- **Milestone table in multi-version** - Tabular overview when multiple milestones exist.

### Sources for PAUL Additions
- Scope separation: Standard PRD practice for clear deliverable tracking
- Milestone table: Dashboard pattern for quick progress visibility
