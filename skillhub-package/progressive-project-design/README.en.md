# Progressive Project Design

[Simplified Chinese](README.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

A progressive project-design Skill for AI coding agents. It combines Just-in-Time Design, vertical slices, and code-to-document calibration so documentation evolves with implementation without turning into Big Design Up Front.

## Core principles

> Documentation is an output of decisions, not their starting point.

- **Design on demand:** Detail only what the current decision or slice needs.
- **Align requirements iteratively:** Make material open decisions visible, ask the user, and update the shared summary until the user confirms alignment.
- **Slice-driven delivery:** Design around the smallest runnable, verifiable end-to-end loop.
- **Stop at the current artifact:** Do not pre-design later scope.
- **Calibrate after implementation:** Update documents from code, tests, configuration, and observed behavior.
- **Maintain two-way relationships:** Record code locations, dependencies, and backlinks in module documents.
- **Review and accept with evidence:** Map requirements to acceptance criteria, implementation locations, and verification evidence; use a focused repair workflow for reported defects.
- **Preserve test integrity:** Derive expectations from the confirmed spec, require meaningful assertions, and never weaken checks to manufacture a pass; report actual execution evidence.
- **Keep generated project docs local:** Ignore `.ppd/` in the consuming project's `.gitignore`; do not stage or commit it.

## Progressive loading

`SKILL.md` is the routing entry point. Detailed workflows are split into `references/` and should be loaded only for the current task: initialization, existing-project analysis, directory-structure analysis, requirements, slice planning, verification/backtesting, implementation logs, code review and acceptance, targeted repair, calibration, navigation, and snapshots.

Two required artifacts are part of the workflow:

- Existing projects produce `.ppd/01-overview/project-structure.md` from observed code and configuration. New projects choose a structure only after requirements and technology options are confirmed.
- Every behavior-changing slice plans a success path, relevant boundary and failure/recovery cases, applicable regression cases, and unit-test coverage before implementation. After implementation, tests are selected from the change's impact scope; time-series, trading, recommendation, and model work may use the specialized backtest form.

## State model

| Dimension | States |
|---|---|
| Document maturity | `D0` unregistered → `D1` draft → `D2` approved → `D3` implementing → `D4` calibrated |
| Design depth | `L0` boundary → `L1` current-slice detail → `L2` full relevant detail |

L1 is normally enough to start implementation. Use L2 only when the current work needs edge cases, failure handling, performance, or similar constraints.

## Project documentation

The Skill uses `.ppd/` as its progressive-documentation entry point:

```text
.ppd/
├── README.md
├── 01-overview/
├── 02-architecture/
├── 03-plan/
├── 04-progress/<slice>/
└── 05-modules/
```

On first use, it checks existing structure and creates only the necessary skeleton. Existing codebases use reverse calibration: extract modules, interfaces, data models, dependencies, and the current directory structure from implementation, then document one slice at a time.

## Six-stage rhythm

| Stage | Trigger | Output |
|---|---|---|
| Skeleton | Project initialization | `.ppd/README.md` and minimum directories |
| Requirements | Boundaries are confirmed | Positioning, scope, decisions, and non-goals |
| Solution and spec | Requirements are aligned | Architecture boundaries, confirmed feature spec, acceptance scenarios, and slice mapping |
| Slice start | A slice is ready to begin | Relevant technology decisions (if any), module L1 documents, verification cases, roadmap entry |
| Implementation | A meaningful change occurs | Impact scope, selected tests, commands and results, decision reason, and remaining issues; review and requirement acceptance when appropriate |
| Calibration | Slice implementation finishes | D3→D4, code locations, deviations, and backlinks |

## Verification and tests

For behavior changes, add or update unit tests for changed logic and relevant boundary or failure cases. If behavior cannot reasonably be isolated in a unit test, use the most appropriate available test level and record why. After implementation, analyze affected units, interfaces, dependencies, and callers; run the changed unit's tests and relevant regressions, widening to the affected module or package suite for cross-unit changes. Record the scope, test choice, commands, results, and evidence. If a test cannot be authored or run, record why, alternative verification, and remaining risk. Documentation-only changes use applicable documentation checks instead of unit tests. For risk-appropriate review and a requirement-to-evidence acceptance matrix, see [review and acceptance](references/review-and-acceptance.md); for a reported defect, see [targeted repair](references/targeted-repair.md). A repair remains pending until verification evidence is available.

## Use cases

- Establish lightweight, evolvable architecture documentation for a new project.
- Summarize an existing project’s directory structure and implementation boundaries.
- Adopt the method in an existing project while preserving README, ADR, and RFC conventions.
- Plan verifiable end-to-end vertical slices.
- Define acceptance, replay, regression, or backtest cases before implementation.
- Add unit tests for behavior changes and select regression tests from the impact scope.
- Determine the next task from the roadmap, module L1 documents, verification cases, and code.
- Investigate drift between implementation and documentation.
- Summarize a finished slice and calibrate affected modules.

## Installation

Use this prompt in your AI coding agent:

```text
Install the Progressive Project Design Skill from https://github.com/xiaoda001/progressive-project-design
```

## Usage steps

1. Open the project in your coding agent.
2. Invoke this Skill using the active coding agent's supported entry point and describe the task. Say whether this is a new or existing project.
3. Review the current stage's output. The Skill checks `.ppd/` and available project evidence, then handles only the next relevant stage.
4. When ready, invoke it again with the next task, such as planning a slice, implementing it, or calibrating its documents.

Example prompts:

```text
Inspect this project's progressive-design state and report the smallest justified next step
Summarize the current project’s directory structure
Create the minimum .ppd documentation skeleton for this new project
Plan the next vertical slice and define its verification cases
Review this slice and map each requirement to its acceptance evidence
Diagnose this failure, find the root cause, and make the smallest verified repair
Calibrate the module documents affected by the current slice
```

Skill invocation varies by coding agent. Use the entry point supported by the active agent; the workflow does not depend on a specific command format or product configuration.

## Repository structure

```text
progressive-project-design/
├── SKILL.md
├── agents/
├── references/
├── README.md
├── README.en.md
├── README.ja.md
└── README.ko.md
```

## License

[MIT License](LICENSE)
