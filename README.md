# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

一个面向 AI 编程代理的渐进式项目设计 Skill。它通过 Just-in-Time Design（按需设计）、垂直切片以及代码↔文档校准，让项目文档随着实现演进，同时避免 Big Design Up Front。

## 核心原则

> 文档是决策的产物，不是决策的起点。

- **按需设计**：只细化当前决策或当前切片需要的内容。
- **切片驱动**：以端到端可运行、可验证的最小闭环为设计单位。
- **及时停笔**：完成当前阶段产出后停止，不提前设计后续范围。
- **实现校准**：切片完成后，用代码、测试、配置和运行行为更新文档。
- **双向关系**：在模块文档中维护接口代码位置、依赖和反向链接。

## 状态模型

| 维度 | 状态 |
|---|---|
| 文档成熟度 | `D0` 未设计 → `D1` 草稿 → `D2` 可开工 → `D3` 实现中 → `D4` 已校准 |
| 设计深度 | `L0` 边界 → `L1` 当前切片所需 → `L2` 完整细化 |

通常以 L1 开工；只有当前实现确实需要边界情况、异常处理、性能等约束时才进入 L2。

## 项目文档体系

Skill 使用 `.ppd/` 作为渐进式文档入口：

```text
.ppd/
├── README.md
├── 01-overview/
├── 02-architecture/
├── 03-plan/
├── 04-progress/
│   └── <slice>/
└── 05-modules/
```

首次使用时检查现有结构，只建立必要骨架。已有代码的项目采用逆向校准：从当前实现提取模块、接口、数据模型和依赖，再逐个切片补齐文档。

## 五阶段节奏

| 阶段 | 触发点 | 产出 |
|---|---|---|
| 骨架 | 项目初始化 | `.ppd/README.md` 和最小目录 |
| 需求 | 边界确认后 | 项目定位、范围、关键决策和非目标 |
| 切片启动 | 当前切片准备实现 | 技术选择、相关模块 L1、路线图登记 |
| 实现中 | 发生有意义的变更 | 简短开发日志、决策原因和遗留事项 |
| 校准 | 切片实现完成 | D3→D4、代码位置、偏差和反向链接 |

## 适用场景

- 为新项目建立轻量、可演进的架构文档；
- 将已有项目迁移到渐进式设计，同时保留现有 README、ADR 和 RFC；
- 规划端到端垂直切片；
- 根据路线图、模块 L1 文档和代码确定下一项任务；
- 排查实现与文档之间的偏差；
- 在切片完成后生成回顾并校准模块文档。

## 安装

仓库根目录就是完整的 [Agent Skills](https://agentskills.io/) 技能目录。将仓库克隆到对应 Agent 的全局 Skill 目录：

| Agent | Windows | macOS / Linux |
|---|---|---|
| Codex | `%USERPROFILE%\.codex\skills\progressive-project-design` | `~/.codex/skills/progressive-project-design` |
| Claude Code | `%USERPROFILE%\.claude\skills\progressive-project-design` | `~/.claude/skills/progressive-project-design` |
| Qoder CLI | `%USERPROFILE%\.qoder\skills\progressive-project-design` | `~/.qoder/skills/progressive-project-design` |
| TRAE | `%USERPROFILE%\.trae\skills\progressive-project-design` | `~/.trae/skills/progressive-project-design` |
| TRAE CN | `%USERPROFILE%\.trae-cn\skills\progressive-project-design` | `~/.trae-cn/skills/progressive-project-design` |

PowerShell 示例：

```powershell
git clone https://github.com/xiaoda001/progressive-project-design.git `
  "$env:USERPROFILE\.codex\skills\progressive-project-design"
```

macOS / Linux 示例：

```bash
git clone https://github.com/xiaoda001/progressive-project-design.git \
  ~/.claude/skills/progressive-project-design
```

安装后重新启动 Agent，或使用其 Skill 刷新功能。更新已安装版本：

```bash
git -C <agent-skill-directory>/progressive-project-design pull --ff-only
```

## 使用示例

```text
$progressive-project-design 检查这个项目的渐进式设计状态，并告诉我最小的下一步
$progressive-project-design 为这个新项目建立最小的 .ppd 文档骨架
$progressive-project-design 根据当前路线图规划下一个垂直切片
$progressive-project-design 校准当前切片涉及的模块文档
```

Claude Code 使用斜杠形式，例如：

```text
/progressive-project-design 检查当前项目状态
```

## 仓库结构

```text
progressive-project-design/
├── SKILL.md
├── agents/openai.yaml
├── references/
│   ├── migration.md
│   └── templates.md
├── README.md
├── README.en.md
├── README.ja.md
└── README.ko.md
```

## 许可证

[MIT License](LICENSE)
