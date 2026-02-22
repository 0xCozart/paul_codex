# PAUL Codex Plugin Design

Date: 2026-02-22

## Goal
Add Codex support while preserving the existing Claude Code installer. Codex support must:
- Expose PAUL commands as Codex prompts ("/paul:*" UX)
- Bundle PAUL assets into a single Codex skill
- Remove GSD assets during Codex install

## Architecture
The installer will support two install targets:
- Claude Code (existing behavior)
- Codex (new behavior)

Codex install has two outputs:
1. Prompts: `~/.codex/prompts/paul-*.md`
2. Skill bundle: `~/.codex/skills/paul/` containing `SKILL.md`, `workflows/`, `templates/`, `references/`, `rules/`

The prompts will reference the bundled skill assets using `@~/.codex/skills/paul/...` paths.

## Components
- `bin/install.js`
  - Add `--codex` flag (and help text)
  - Add install path for Codex prompts and skill bundle
  - Add GSD cleanup step during Codex install
- `src/commands/*.md`
  - Source of command prompts; converted into Codex prompt format during install
- New template for Codex prompt frontmatter
- New `src/skills/paul/SKILL.md` (or generated at install) to define the single skill

## Data Flow
1. Installer determines target (`--global/--local` for Claude, `--codex` for Codex).
2. For Codex:
   - Copy workflows/templates/references/rules into `~/.codex/skills/paul/`
   - Generate prompt files in `~/.codex/prompts/` from `src/commands/*.md`
   - Delete `~/.codex/prompts/gsd-*.md`
   - Delete `~/.codex/get-shit-done/`

## Error Handling
- If `--codex` is combined with `--local` or `--global`, fail with a clear error.
- If any file copy fails, surface the error and exit non-zero.
- GSD deletion should ignore missing paths (no error if already removed).

## Testing
- Manual verification:
  - Run `node bin/install.js --codex` in a clean environment
  - Confirm `~/.codex/prompts/paul-*.md` exist and include correct frontmatter
  - Confirm `~/.codex/skills/paul/` contains expected subdirectories
  - Confirm GSD prompts and directory are removed
  - Open a Codex session and run a `/paul:*` command to verify prompt activation

## Decisions
- Keep Claude installer unchanged; add Codex as a new target.
- Use a single Codex skill bundle and separate prompt files.
- Remove GSD assets as part of Codex install.
