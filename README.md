# Progressive Project Design

[中文](README.zh.md) | English

A progressive project-design Skill for AI coding agents. It combines Just-in-Time Design, vertical slices, and code-to-document calibration so documentation evolves with implementation without turning into Big Design Up Front.

## Core principles

> Documentation is an output of decisions, not their starting point.

- **Design on demand:** Detail only what the current decision or slice needs.
- **Slice-driven delivery:** Design around the smallest runnable, verifiable end-to-end loop.
- **Stop at the current artifact:** Do not pre-design later scope.
- **Calibrate after implementation:** Update documents from code, tests, configuration, and observed behavior.
- **Maintain two-way relationships:** Record code locations, dependencies, and backlinks in module documents.

## Progressive loading

`SKILL.md` is the routing entry point. Detailed workflows are split into `references/` and should be loaded only for the current task: initialization, existing-project analysis, directory-structure analysis, requirements, slice planning, verification/backtesting, implementation logs, calibration, navigation, and snapshots.

Two required artifacts are part of the workflow:

- Existing projects produce `.ppd/01-overview/project-structure.md` from observed code and configuration. New projects choose a structure only after requirements and technology options are confirmed.
- Every slice defines verification cases before implementation: a success path, boundary case, failure/recovery case, and relevant regression case. Time-series, trading, recommendation, and model work may use the specialized backtest form.

## State model

| Dimension | States |
|---|---|
| Document maturity | `D0` registered → `D1` draft → `D2` ready → `D3` implementing → `D4` calibrated |
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

## Five-stage rhythm

| Stage | Trigger | Output |
|---|---|---|
| Skeleton | Project initialization | `.ppd/README.md` and minimum directories |
| Requirements | Boundaries are confirmed | Positioning, scope, decisions, and non-goals |
| Slice start | A slice is ready to begin | Required technology choices, module L1 documents, verification cases, roadmap entry |
| Implementation | A meaningful change occurs | Short log, decision reason, verification result, and remaining issues |
| Calibration | Slice implementation finishes | D3→D4, code locations, deviations, and backlinks |

## Use cases

- Establish lightweight, evolvable architecture documentation.
- Summarize an existing project's directory structure and implementation boundaries.
- Adopt the method in an existing project while preserving README, ADR, and RFC conventions.
- Plan verifiable end-to-end vertical slices.
- Define acceptance, replay, regression, or backtest cases before implementation.
- Determine the next task from the roadmap, module L1 documents, verification cases, and code.
- Investigate drift between implementation and documentation.
- Summarize a finished slice and calibrate affected modules.

## Installation

The repository root is a complete [Agent Skills](https://agentskills.io/) directory. Clone it into the global Skill directory used by your agent:

| Agent | Windows | macOS / Linux |
|---|---|---|
| Codex | `%USERPROFILE%\.codex\skills\progressive-project-design` | `~/.codex/skills/progressive-project-design` |
| Claude Code | `%USERPROFILE%\.claude\skills\progressive-project-design` | `~/.claude/skills/progressive-project-design` |
| Qoder CLI | `%USERPROFILE%\.qoder\skills\progressive-project-design` | `~/.qoder/skills/progressive-project-design` |

PowerShell example:

```powershell
git clone https://github.com/xiaoda001/progressive-project-design.git `
  "$env:USERPROFILE\.codex\skills\progressive-project-design"
```

Update an installed copy with:

```bash
git -C <agent-skill-directory>/progressive-project-design pull --ff-only
```

## Usage examples

```text
$progressive-project-design Inspect this project's progressive-design state and report the smallest justified next step
$progressive-project-design Summarize the current project's directory structure
$progressive-project-design Plan the next vertical slice and define its verification cases
$progressive-project-design Calibrate the module documents affected by the current slice
```

## Repository structure

```text
progressive-project-design/
├── SKILL.md
├── agents/openai.yaml
├── references/
├── README.md
└── README.zh.md
```

## License

[MIT License](LICENSE)
