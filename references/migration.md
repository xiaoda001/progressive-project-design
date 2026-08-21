# Adopt the method in an existing project

Use this procedure only when the user asks to adopt, initialize, reorganize, or migrate documentation in a project that already contains documentation.

## Preserve first

1. Read repository instructions and identify the established documentation entry point.
2. Inventory existing overview, architecture, ADR/RFC, roadmap, module, and progress documents.
3. Map existing material to this method without moving or renaming files by default.
4. Identify contradictions, duplicate sources of truth, stale claims, and missing ownership.
5. Propose the smallest migration before editing.

## Mapping guidance

| Existing artifact | Progressive-design role |
|---|---|
| README/product brief | Project overview |
| ADR/RFC | Technology or architecture decision; retain its native format |
| Milestone/epic | Candidate vertical slice; verify that it is user-observable |
| Component document | Module document; add D/L metadata only if compatible |
| Changelog/PR history | Evidence source, not automatically a slice log |
| Test plan/runbook | Acceptance or calibration evidence |

## Editing rules

- Do not relocate files merely to match the recommended numbered directory layout.
- Do not create a second roadmap or module index when an equivalent source of truth exists.
- Add links or a thin index instead of duplicating content.
- Do not label legacy material D4 until it has been checked against current implementation and evidence.
- When existing terminology conflicts with D/L/slice terminology, prefer the repository's terminology and record the mapping once.
- Present proposed renames, moves, or deletions to the user before performing them.

## Migration result

Report:

- retained sources of truth;
- new files or metadata added;
- unresolved contradictions;
- active slice and acceptance evidence, if known;
- the next smallest documentation action.

