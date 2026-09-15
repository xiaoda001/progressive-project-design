---
name: progressive-project-design
description: Guides AI coding agents through progressive, slice-driven project design and code-to-document calibration. Use for project initialization, existing-project documentation, architecture decisions, vertical slices, verification cases, next-task navigation, and documentation calibration.
---

# Progressive Project Design

Always respond in the user's language. This skill treats documentation as an output of decisions, not as Big Design Up Front.

## Operating principles

- Design only what the current decision or vertical slice needs.
- Use the smallest runnable, verifiable end-to-end slice as the planning unit.
- Keep uninvolved modules at D0; do not pre-design later scope.
- Stop after the current stage's artifact. Continue only when a new trigger exists.
- Treat existing code as the source of truth during reverse calibration.
- Keep project documentation in Git by default. Do not add `.ppd/` to `.gitignore` unless the user or project policy explicitly requires it.

## Status model

| Dimension | Values | Meaning |
|---|---|---|
| Documentation maturity | D0 → D1 → D2 → D3 → D4 | unregistered → draft → approved → implementing → calibrated |
| Design depth | L0 → L1 → L2 | boundary → current-slice detail → full relevant detail |

Use `D4-reverse-engineered` for documentation extracted from implemented code until its scope and behavior have been checked. Use L2 only when the current work requires edge cases, failure handling, performance, or similar constraints.

## Progressive disclosure and routing

Read only the reference needed for the current task. Do not load every reference by default.

| User intent or project state | Read next |
|---|---|
| First activation or missing `.ppd/` | [initialization.md](references/initialization.md), then [directory-structure.md](references/directory-structure.md) |
| Existing project without reliable `.ppd/` | [migration.md](references/migration.md), [existing-project.md](references/existing-project.md), then [directory-structure.md](references/directory-structure.md) |
| Confirming requirements | [requirements-confirmation.md](references/requirements-confirmation.md) |
| Planning or starting a slice | [slice-planning.md](references/slice-planning.md), [verification-and-backtest.md](references/verification-and-backtest.md) |
| Implementing a slice | [implementation-log.md](references/implementation-log.md) |
| Asking what to do next | [task-navigation.md](references/task-navigation.md) |
| Slice completed or docs drifted | [calibration.md](references/calibration.md) |
| Asking for project state | [project-snapshot.md](references/project-snapshot.md) |
| Creating or updating a `.ppd/` artifact | Read only the matching section in [templates.md](references/templates.md); for structure or verification artifacts also read [structure-and-verification-templates.md](references/structure-and-verification-templates.md) |

## First activation decision tree

1. Check whether the project root contains `.ppd/`.
2. If it is a new project, create only the skeleton and stop.
3. If code already exists and `.ppd/` is missing or stale, perform one reverse-analysis pass and create clearly marked draft/reverse-engineered artifacts; do not redesign implemented behavior.
4. If `.ppd/` is healthy, read the project snapshot and continue at the current stage; do not repeat initialization.

The initial directory skeleton is:

```text
.ppd/
├── README.md
├── 01-overview/
├── 02-architecture/
├── 03-plan/
├── 04-progress/
└── 05-modules/
```

Do not create future slice directories until the slice is registered in the roadmap.

## Required slice invariant

Before implementing a slice, record both:

- a completion condition: what can run or be demonstrated;
- verification cases: at least the main success path, a boundary case, a failure case, and any required regression case.

For financial, time-series, recommendation, or model work, verification cases may be called backtests and must specify a fixed dataset, parameters, metrics, and reproducible execution command. For ordinary business software, use verification, acceptance, replay, or regression cases instead.

## Decision standard

Before writing any document, answer:

> Who will read it? When will they read it? What decision will they make after reading it?

If those answers are unclear, do not create the document yet.

## Relationship invariants

- `.ppd/README.md` is the single navigation entry point.
- Module documents contain responsibility, interfaces, dependencies, code locations, and backlinks.
- Code links must use `path#line` and be updated during calibration.
- D4 claims require implementation evidence; a filename alone is not evidence.
- A calibration aligns existing scope; it must not silently add new scope.
