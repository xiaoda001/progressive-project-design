# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

AI 코딩 에이전트를 위한 점진적 프로젝트 설계 Skill입니다. Just-in-Time Design, 수직 슬라이스, 코드↔문서 보정을 결합하여 과도한 선행 설계를 피하면서 문서가 구현과 함께 발전하도록 합니다.

## 핵심 원칙

> 문서는 의사결정의 시작점이 아니라 결과물입니다.

- 현재 결정이나 슬라이스에 필요한 내용만 설계
- 실행하고 검증할 수 있는 최소 엔드투엔드 슬라이스를 단위로 사용
- 현재 산출물이 완성되면 멈추고 이후 범위를 미리 설계하지 않음
- 코드, 테스트, 설정 및 실행 결과를 기반으로 문서 보정
- 모듈 문서에 코드 위치, 의존성 및 역링크 유지

## 상태 모델

| 차원 | 상태 |
|---|---|
| 문서 성숙도 | `D0` 등록 → `D1` 초안 → `D2` 구현 준비 → `D3` 구현 중 → `D4` 보정 완료 |
| 설계 깊이 | `L0` 경계 → `L1` 현재 슬라이스에 필요 → `L2` 필요한 상세 설계 완료 |

일반적으로 L1에서 구현을 시작하고 현재 작업에 예외 처리, 성능 등의 제약이 실제로 필요할 때만 L2로 진행합니다.

## 문서 체계

Skill은 `.ppd/`를 점진적 문서의 단일 진입점으로 사용합니다.

```text
.ppd/
├── README.md
├── 01-overview/
├── 02-architecture/
├── 03-plan/
├── 04-progress/<slice>/
└── 05-modules/
```

기존 프로젝트에서는 현재 코드에서 모듈, 인터페이스, 데이터 모델 및 의존성을 추출하고 한 번에 하나의 슬라이스를 역방향으로 보정합니다.

## 5단계 리듬

| 단계 | 시점 | 산출물 |
|---|---|---|
| 골격 | 프로젝트 초기화 | `.ppd/README.md`와 최소 디렉터리 |
| 요구사항 | 경계 확인 후 | 목적, 범위, 결정 및 비목표 |
| 슬라이스 시작 | 구현 준비 시 | 필요한 기술 선택, 모듈 L1, 로드맵 |
| 구현 중 | 의미 있는 변경 | 짧은 로그, 결정 이유, 남은 문제 |
| 보정 | 슬라이스 완료 | D3→D4, 코드 위치, 차이 및 역링크 |

## 설치

저장소 루트가 완전한 [Agent Skills](https://agentskills.io/) 디렉터리입니다.

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

업데이트:

```bash
git -C <agent-skill-directory>/progressive-project-design pull --ff-only
```

## 사용 예시

```text
$progressive-project-design 이 프로젝트의 점진적 설계 상태와 가장 작은 다음 작업을 확인하세요
$progressive-project-design 새 프로젝트용 최소 .ppd 골격을 만드세요
$progressive-project-design 현재 로드맵에서 다음 수직 슬라이스를 계획하세요
$progressive-project-design 현재 슬라이스와 관련된 모듈 문서를 보정하세요
```

Claude Code에서는 `/progressive-project-design 현재 프로젝트 상태를 확인하세요`처럼 호출합니다.

## 저장소 구조

```text
progressive-project-design/
├── SKILL.md
├── agents/openai.yaml
├── references/migration.md
├── references/templates.md
├── README.md
├── README.en.md
├── README.ja.md
└── README.ko.md
```

## 라이선스

[MIT License](LICENSE)
