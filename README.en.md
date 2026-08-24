# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

A progressive project-design Skill for AI coding agents. It combines Just-in-Time Design, vertical slices, and code-to-document calibration to keep evolving projects clear, actionable, and free from unnecessary up-front design.

## Purpose

Large up-front documents quickly drift once implementation begins and burden agents with irrelevant context. Progressive Project Design prepares only the information required for the current decision and vertical slice, then calibrates the documentation against code, tests, configuration, and observed runtime behavior.

Use it to:

- establish lightweight, evolvable architecture documentation for a new project;
- migrate an existing project while preserving its ADRs, RFCs, and documentation conventions;
- split requirements into observable, testable end-to-end slices;
- identify and advance one smallest safe task at a time;
- detect drift between implementation and design documentation;
- archive completed slice history to reduce active-context noise.

## Core capabilities

### Short-action workflow

| Action | Purpose |
|---|---|
| `status` / `状态` | Read-only inspection of the project, documents, active slice, drift, and evidence |
| `init` / `初始化` | Create or migrate the minimum progressive-documentation skeleton |
| `requirement` / `需求` | Clarify the observable outcome and classify a requirement |
| `change` / `变更` | Analyze impact on slices, interfaces, data, and dependencies |
| `plan` / `规划` | Plan the next vertical slice |
| `prepare [Sx]` / `准备 [Sx]` | Prepare a selected slice for implementation |
| `next` / `下一步` | Determine the smallest implementation task from current evidence |
| `go` / `推进` | Implement and verify one smallest safe, unblocked task |
| `calibrate [Sx]` / `校准 [Sx]` | Update documentation against implementation evidence |
| `archive [Sx]` / `归档 [Sx]` | Verify completion and archive historical slice artifacts |

### Three-dimensional state model

- Document maturity: `D0` (registered) through `D4` (calibrated against implementation).
- Design depth: `L0` (boundary) through `L2` (relevant non-functional constraints).
- Slice execution: `planned`, `ready`, `in-progress`, `blocked`, `calibrating`, or `done`.

### Evidence-driven calibration and cold archives

A document reaches `D4` only after code, tests, configuration, migrations, and runnable entry points have been checked. Completed slice material can move into cold storage; routine work reads active truth first and loads history only when regressions, compatibility, migrations, or past decisions make it relevant.

## Benefits

- Reduces over-design by preparing only the L1 information needed by the current slice.
- Keeps active context compact by moving completed history into cold archives.
- Controls documentation drift through implementation and verification evidence.
- Protects in-progress work by classifying requirement changes before changing scope.
- Adapts to existing README, ADR, RFC, roadmap, and module conventions.
- Separates read-only analysis, documentation writes, and code implementation authority.
- Keeps each vertical slice tied to an observable outcome and acceptance evidence.

## Installation

The repository root is a complete [Agent Skills](https://agentskills.io/) directory. `SKILL.md` is the shared entry point, `references/` is loaded on demand, and `agents/openai.yaml` adds optional Codex UI metadata.

Clone the repository into your agent's global Skill directory:

| Agent | Windows | macOS / Linux |
|---|---|---|
| Codex | `%USERPROFILE%\.codex\skills\progressive-project-design` | `~/.codex/skills/progressive-project-design` |
| Claude Code | `%USERPROFILE%\.claude\skills\progressive-project-design` | `~/.claude/skills/progressive-project-design` |
| Qoder CLI | `%USERPROFILE%\.qoder\skills\progressive-project-design` | `~/.qoder/skills/progressive-project-design` |
| TRAE | `%USERPROFILE%\.trae\skills\progressive-project-design` | `~/.trae/skills/progressive-project-design` |
| TRAE CN | `%USERPROFILE%\.trae-cn\skills\progressive-project-design` | `~/.trae-cn/skills/progressive-project-design` |

PowerShell example for Codex:

```powershell
git clone https://github.com/xiaoda001/progressive-project-design.git `
  "$env:USERPROFILE\.codex\skills\progressive-project-design"
```

macOS / Linux example for Qoder:

```bash
git clone https://github.com/xiaoda001/progressive-project-design.git \
  ~/.qoder/skills/progressive-project-design
```

Restart the agent or refresh its Skill discovery. Qoder CLI supports `/skills reload`. To update an installed copy:

```bash
git -C <skill-directory>/progressive-project-design pull --ff-only
```

## Usage

```text
$progressive-project-design status
$progressive-project-design init
$progressive-project-design requirement Add team invitations
$progressive-project-design prepare S1
$progressive-project-design go
$progressive-project-design calibrate S1
$progressive-project-design archive S1
```

Start with `status` in an existing project. If the progressive documentation set is absent, explicitly run `init`. In Claude Code, use `/progressive-project-design status`; matching requests can also load the Skill automatically.

## Repository structure

```text
progressive-project-design/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── migration.md
    └── templates.md
```

## License

[MIT License](LICENSE)
