---
name: progressive-project-design
description: Guides coding agents across products through progressive, slice-driven project design and code-to-document calibration. Use for project initialization, existing-project documentation, architecture decisions, vertical slices, verification cases, agent-enabled delivery workflows, next-task navigation, and documentation calibration.
slug: progressive-project-design
displayName: 渐进式项目设计
version: 1.3.0
summary: 以垂直切片、按需设计和代码文档校准帮助不同编程代理渐进式设计项目，并规划 agent 交付、验证与影响范围回归。
license: MIT
---

# Progressive Project Design

Always respond in the user's language. This skill treats documentation as an output of decisions, not as Big Design Up Front.

## Operating principles

- Design only what the current decision or vertical slice needs.
- Use the smallest runnable, verifiable end-to-end slice as the planning unit.
- Keep uninvolved modules at D0; do not pre-design later scope.
- Stop after the current stage's artifact. Continue only when a new trigger exists.
- Treat existing code as the source of truth during reverse calibration.
- Treat agent-enabled delivery as an end-to-end workflow: capture intent, review a bounded plan, verify outputs, enforce risk-appropriate human decisions, and feed operational evidence back into planning.
- Keep the workflow portable across coding agents. Define shared artifacts, decisions, and checks independently of any agent's product-specific files or features; adapt only the execution mechanism to the active agent's documented capabilities.
- Confirm requirements through an iterative question-and-validation loop. Make material decision branches visible, update the shared understanding after each answer, and do not treat silence as approval.
- Treat tests as contract evidence, not a green-check target: derive expectations from the confirmed spec, require meaningful assertions and risk-relevant boundaries, and never invent or misstate execution results.
- Calibrate only affected documents; separate observed implementation facts from accepted intent, expose unresolved mismatches, and withhold D4 when applicable verification is pending.
- Keep generated `.ppd/` project documentation local. Ensure the project-root `.gitignore` excludes `.ppd/`, preserving existing rules or creating the file when needed. Do not stage, commit, or upload `.ppd/`. If `.ppd/` files are already tracked, report that ignore rules do not untrack them; do not change the Git index without an explicit request.

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
| Turning aligned requirements into architecture, a feature spec, and functional slices | [solution-design-and-spec.md](references/solution-design-and-spec.md), then [slice-planning.md](references/slice-planning.md) |
| Planning or starting a slice | [slice-planning.md](references/slice-planning.md), [verification-and-backtest.md](references/verification-and-backtest.md) |
| Implementing a slice | [implementation-log.md](references/implementation-log.md) |
| Reviewing or accepting an implementation | [review-and-acceptance.md](references/review-and-acceptance.md) |
| Diagnosing and fixing a reported defect | [targeted-repair.md](references/targeted-repair.md) |
| Asking what to do next | [task-navigation.md](references/task-navigation.md) |
| Designing an AI-agent delivery workflow, evaluating agent behavior, or closing the production-feedback loop | [agent-delivery-loop.md](references/agent-delivery-loop.md), then load only the relevant slice, verification, review, or calibration reference |
| Slice completed or docs drifted | [calibration.md](references/calibration.md) |
| Asking for project state | [project-snapshot.md](references/project-snapshot.md) |
| Creating or updating a `.ppd/` artifact | Read only the matching section in [templates.md](references/templates.md); for structure or verification artifacts also read [structure-and-verification-templates.md](references/structure-and-verification-templates.md) |

## First activation decision tree

1. Check whether the project root contains `.ppd/`.
2. Ensure the project-root `.gitignore` excludes `.ppd/`, preserving existing ignore rules or creating the file when needed. If `.ppd/` files are already tracked, report this because ignore rules do not untrack existing files; do not change the Git index without an explicit request.
3. If it is a new project, create only the skeleton and stop.
4. If code already exists and `.ppd/` is missing or stale, perform one reverse-analysis pass and create clearly marked draft/reverse-engineered artifacts; do not redesign implemented behavior.
5. If `.ppd/` is healthy, read the project snapshot and continue at the current stage; do not repeat initialization.

For new features or substantial changes, use this order after requirements align: define architecture boundaries, write and confirm the feature spec, identify high-level acceptance scenarios, decompose the spec into functional vertical slices, then plan and implement one slice at a time. Keep architecture at L0/L1 for unstarted scope; deepen only the active slice. Small fixes may use a concise inline spec and go directly to targeted repair.

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

Before implementing a slice, record:

- a completion condition: what can run or be demonstrated;
- applicable verification cases: the main success path, a relevant boundary case, a failure/recovery case, and a regression case when prior behavior exists;
- planned unit-test coverage for new or changed behavior. Name the expected test file/case and command when known; if implementation details are not yet known, mark them as planned or `TBD` and finalize them during implementation.

Add or update unit tests for behavior changes, following repository conventions and covering changed logic plus relevant boundary and failure behavior. Derive test expectations from the confirmed contract, not solely from implementation. Assertions must detect meaningful regressions; do not weaken or skip checks just to obtain a passing run. If the behavior cannot reasonably be isolated in a unit test, use the most appropriate available test level and record why. Do not add a new test framework outside the slice's scope without justification. Read [verification-and-backtest.md](references/verification-and-backtest.md) for test-integrity checks.

After implementation, analyze the impact scope of code or behavior changes before verification. Identify changed units, interfaces, dependencies, existing callers, and prior behavior. For a change contained within one unit, run that unit's tests and relevant regressions. For cross-unit or interface changes, include affected dependents and the relevant module or package suite. Use the full repository suite when a shared/core contract affects multiple areas, or when no bounded suite provides meaningful coverage; if impact remains unclear after investigation, run the broadest bounded relevant suite and explain the choice. For documentation-only changes, do not run unit tests; use applicable documentation checks when available. For configuration-only changes, select tests according to the behavior the configuration can affect. Log the scope, selection rationale, commands, results, evidence, and gaps. If a test cannot be authored or run, record why, alternative verification, and remaining risk; never report an unrun test as passing.

For financial, time-series, recommendation, or model work, verification cases may be called backtests and must specify a fixed dataset, parameters, metrics, and reproducible execution command. For ordinary business software, use verification, acceptance, replay, or regression cases instead. Run unit tests selected from impact analysis when code behavior changes; documentation-only changes use applicable documentation checks instead.

After implementation, use the review and acceptance workflow when the task or risk calls for it. Review findings first and keep fixes separate unless they are within the authorized task. Map each requirement to an acceptance criterion, implementation location, evidence, and status. For a reported defect, use the targeted-repair workflow to establish a reproducer, validate a root-cause hypothesis, make the smallest justified change, and leave the result pending until verification evidence exists. Ask the user only when an unresolved choice changes scope, behavior, or another material project decision.

## Decision standard

Before writing any document, answer:

> Who will read it? When will they read it? What decision will they make after reading it?

If those answers are unclear, do not create the document yet.

## Agent portability

This Skill is for coding agents across products, including Codex, Claude Code, Trae, and others. Treat the workflow and project artifacts as the portable contract. Do not require a specific agent, model, configuration filename, plugin, tool protocol, or vendor feature. Before using an agent-specific capability, confirm it is available in the active environment and provide a tool-agnostic fallback when practical. Keep project policy and source-of-truth artifacts in the project or its established systems; agent-specific instructions may only adapt how the shared workflow is executed and must not redefine it.

## Relationship invariants

- `.ppd/README.md` is the single navigation entry point.
- Module documents contain responsibility, interfaces, dependencies, code locations, and backlinks.
- Code links must use `path#line` and be updated during calibration.
- D4 claims require implementation evidence; a filename alone is not evidence.
- A calibration aligns only affected documents with accepted scope and evidence; it must not silently add scope, hide spec mismatches, or promote unverified behavior to D4.
