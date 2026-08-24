# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

AI 코딩 에이전트를 위한 점진적 프로젝트 설계 Skill입니다. Just-in-Time Design, 수직 슬라이스, 코드와 문서의 보정을 결합하여 지속적으로 변화하는 프로젝트를 명확하고 실행 가능한 상태로 유지하고 과도한 선행 설계를 방지합니다.

## 용도

대규모 선행 문서는 구현이 시작된 뒤 빠르게 부정확해지고 에이전트에 불필요한 컨텍스트를 제공합니다. 이 Skill은 현재 결정과 수직 슬라이스에 필요한 정보만 준비하고 코드, 테스트, 설정, 실행 결과를 근거로 문서를 보정합니다.

- 새 프로젝트에 가볍고 발전 가능한 아키텍처 문서 체계 구축
- 기존 ADR, RFC 및 문서 규칙을 유지하면서 기존 프로젝트 마이그레이션
- 요구사항을 관찰하고 검증할 수 있는 엔드투엔드 슬라이스로 분할
- 가장 작고 안전한 다음 작업을 한 번에 하나씩 진행
- 구현과 설계 문서 사이의 불일치 탐지
- 완료된 슬라이스 기록을 보관하여 활성 컨텍스트 축소

## 핵심 기능

### 짧은 액션 워크플로

| 액션 | 목적 |
|---|---|
| `status` / `状态` | 프로젝트, 문서, 활성 슬라이스, 불일치 및 증거를 읽기 전용으로 검사 |
| `init` / `初始化` | 최소 점진적 문서 구조 생성 또는 마이그레이션 |
| `requirement` / `需求` | 관찰 가능한 결과를 명확히 하고 요구사항 분류 |
| `change` / `变更` | 슬라이스, 인터페이스, 데이터 및 의존성 영향 분석 |
| `plan` / `规划` | 다음 수직 슬라이스 계획 |
| `prepare [Sx]` / `准备 [Sx]` | 선택한 슬라이스를 구현 준비 상태로 전환 |
| `next` / `下一步` | 현재 증거에서 가장 작은 구현 작업 결정 |
| `go` / `推进` | 안전하고 차단되지 않은 최소 작업 하나를 구현하고 검증 |
| `calibrate [Sx]` / `校准 [Sx]` | 구현 증거에 따라 문서 갱신 |
| `archive [Sx]` / `归档 [Sx]` | 완료 조건을 확인하고 슬라이스 기록 보관 |

### 3차원 상태 모델

- 문서 성숙도: `D0`(등록)부터 `D4`(구현과 보정 완료)
- 설계 깊이: `L0`(경계)부터 `L2`(관련 비기능 제약)
- 슬라이스 실행 상태: `planned`, `ready`, `in-progress`, `blocked`, `calibrating`, `done`

문서는 코드, 테스트, 설정, 마이그레이션 및 실행 진입점을 확인한 뒤에만 `D4`가 됩니다. 완료된 슬라이스는 콜드 아카이브로 이동하며 회귀, 호환성, 마이그레이션 또는 과거 결정이 관련될 때만 읽습니다.

## 장점

- 현재 슬라이스에 필요한 L1 정보만 준비하여 과도한 설계 방지
- 완료된 기록을 콜드 아카이브로 이동하여 컨텍스트 비용 절감
- 구현 및 검증 증거를 통해 문서 불일치 관리
- 범위를 바꾸기 전에 요구사항 변경을 분류하여 진행 중인 작업 보호
- 기존 README, ADR, RFC, 로드맵 및 모듈 문서 규칙에 적응
- 읽기 전용 분석, 문서 변경 및 코드 구현 권한 분리

## 설치

저장소 루트가 완전한 [Agent Skills](https://agentskills.io/) 디렉터리입니다. `SKILL.md`가 공통 진입점이며 `references/`는 필요할 때만 로드됩니다.

| Agent | Windows | macOS / Linux |
|---|---|---|
| Codex | `%USERPROFILE%\.codex\skills\progressive-project-design` | `~/.codex/skills/progressive-project-design` |
| Claude Code | `%USERPROFILE%\.claude\skills\progressive-project-design` | `~/.claude/skills/progressive-project-design` |
| Qoder CLI | `%USERPROFILE%\.qoder\skills\progressive-project-design` | `~/.qoder/skills/progressive-project-design` |
| TRAE | `%USERPROFILE%\.trae\skills\progressive-project-design` | `~/.trae/skills/progressive-project-design` |
| TRAE CN | `%USERPROFILE%\.trae-cn\skills\progressive-project-design` | `~/.trae-cn/skills/progressive-project-design` |

```bash
git clone https://github.com/xiaoda001/progressive-project-design.git \
  ~/.claude/skills/progressive-project-design
```

설치 후 에이전트를 다시 시작하거나 Skill 검색을 새로 고치십시오. 설치된 Skill 업데이트:

```bash
git -C <skill-directory>/progressive-project-design pull --ff-only
```

## 사용 예시

```text
$progressive-project-design status
$progressive-project-design init
$progressive-project-design requirement 팀 초대 기능 추가
$progressive-project-design prepare S1
$progressive-project-design go
$progressive-project-design calibrate S1
$progressive-project-design archive S1
```

기존 프로젝트에서는 먼저 `status`를 실행하십시오. Claude Code에서는 `/progressive-project-design status`로 호출할 수 있습니다.

## 저장소 구조

```text
progressive-project-design/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── migration.md
    └── templates.md
```

## 라이선스

[MIT License](LICENSE)
