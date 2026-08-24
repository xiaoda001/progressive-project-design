# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

一个面向 AI 编程代理的渐进式项目设计 Skill。它用 Just-in-Time Design（按需设计）、垂直切片和代码/文档校准，帮助项目在持续开发中保持清晰、可执行且不过度设计。

## 用途

传统的大而全文档很容易在实现开始后失真，也会给 AI 带来大量无关上下文。Progressive Project Design 只为当前决策和当前垂直切片准备必要信息，并在实现后用代码、测试、配置和运行结果校准文档。

它适合以下场景：

- 为新项目建立轻量、可演进的架构文档；
- 将已有项目迁移到渐进式设计方法，同时保留现有 ADR、RFC 和文档习惯；
- 把需求拆成可观察、可验收的端到端垂直切片；
- 判断当前最小可执行任务，并一次推进一个安全步骤；
- 检查实现与设计文档之间的偏差；
- 在切片完成后归档历史材料，减少日常上下文噪声。

## 核心功能

### 短动作工作流

Skill 提供一组明确的中英文动作：

| 动作 | 作用 |
|---|---|
| `状态` / `status` | 只读检查项目、文档、当前切片、漂移和证据 |
| `初始化` / `init` | 建立或迁移最小的渐进式文档骨架 |
| `需求` / `requirement` | 澄清用户可观察结果并分类需求 |
| `变更` / `change` | 分析变更对切片、接口、数据和依赖的影响 |
| `规划` / `plan` | 规划下一个垂直切片 |
| `准备 [Sx]` / `prepare [Sx]` | 将指定切片准备到可实现状态 |
| `下一步` / `next` | 从当前证据中确定最小实现任务 |
| `推进` / `go` | 实现并验证一个最小、安全、无阻塞任务 |
| `校准 [Sx]` / `calibrate [Sx]` | 对照实现证据更新文档 |
| `归档 [Sx]` / `archive [Sx]` | 验证完成条件并归档历史切片材料 |

### 三维状态模型

文档状态被拆成三个独立维度，避免用一个模糊的“完成度”混在一起：

- 文档成熟度：`D0`（登记）到 `D4`（已与实现校准）；
- 设计深度：`L0`（边界）到 `L2`（关键非功能约束）；
- 切片执行状态：`planned`、`ready`、`in-progress`、`blocked`、`calibrating`、`done`。

### 需求和变更分类

新请求会被归类为澄清、小扩展、独立能力、横切变更或缺陷。Skill 不会把新需求静默塞进正在实现的切片，而是先说明影响和推荐路径。

### 证据驱动校准

只有在检查代码、测试、配置、迁移和可运行入口后，文档才能标记为 `D4`。实现存在但缺少验证时，会被明确标记为“可能完成”，而不是直接宣告完成。

### 冷上下文归档

完成的切片可以进入冷归档。日常操作只读取活跃事实，只有在回归、兼容、迁移或历史决策确实相关时，才按索引逐层加载归档内容。

## 优势

- **减少过度设计**：默认只准备当前切片需要的 L1 信息，L2 仅在风险真实存在时加入。
- **降低上下文成本**：活跃文档保持紧凑，历史材料进入冷归档，AI 不必反复加载全部项目史。
- **控制文档漂移**：以实现和验证证据校准设计，避免文档仅凭文件名或主观判断变成“已完成”。
- **保护进行中的工作**：需求变更先分类、再决定是否调整切片，避免范围在开发中持续膨胀。
- **兼容存量项目**：优先适配已有 README、ADR、RFC、路线图和模块文档，不强制重排目录。
- **动作边界清晰**：只读分析、文档修改和代码实现拥有不同授权边界，降低误改风险。
- **聚焦可交付结果**：垂直切片必须对应用户可观察结果和明确验收证据。

## 安装

本仓库根目录就是一个完整的 [Agent Skills](https://agentskills.io/) 技能目录：`SKILL.md` 是统一入口，`references/` 按需加载，`agents/openai.yaml` 仅为 Codex 提供额外的界面元数据。其他 Agent 会忽略自己不认识的附加文件，因此无需维护多份 Skill。

将仓库克隆到所用 Agent 的全局 Skill 目录：

| Agent | Windows 目录 | macOS / Linux 目录 |
|---|---|---|
| Codex | `%USERPROFILE%\.codex\skills\progressive-project-design` | `~/.codex/skills/progressive-project-design` |
| Claude Code | `%USERPROFILE%\.claude\skills\progressive-project-design` | `~/.claude/skills/progressive-project-design` |
| Qoder CLI | `%USERPROFILE%\.qoder\skills\progressive-project-design` | `~/.qoder/skills/progressive-project-design` |
| TRAE | `%USERPROFILE%\.trae\skills\progressive-project-design` | `~/.trae/skills/progressive-project-design` |
| TRAE CN | `%USERPROFILE%\.trae-cn\skills\progressive-project-design` | `~/.trae-cn/skills/progressive-project-design` |

PowerShell 示例（以 Codex 为例）：

```powershell
git clone https://github.com/xiaoda001/progressive-project-design.git `
  "$env:USERPROFILE\.codex\skills\progressive-project-design"
```

macOS / Linux 示例（以 Qoder 为例）：

```bash
git clone https://github.com/xiaoda001/progressive-project-design.git \
  ~/.qoder/skills/progressive-project-design
```

安装后重新启动 Agent，或使用该 Agent 提供的 Skill 刷新功能。Qoder CLI 可执行 `/skills reload`；TRAE 可在设置中刷新 Skill 发现。更新已安装的 Skill：

```bash
git -C <skill-directory>/progressive-project-design pull --ff-only
```

也可以把整个仓库复制到其他支持 `SKILL.md` / Agent Skills 规范的工具所配置的 Skill 搜索目录。目录名应保持为 `progressive-project-design`。

## 使用示例

```text
$progressive-project-design 状态
$progressive-project-design 初始化
$progressive-project-design 需求 增加团队成员邀请功能
$progressive-project-design 准备 S1
$progressive-project-design 推进
$progressive-project-design 校准 S1
$progressive-project-design 归档 S1
```

建议首次在已有项目中使用时先运行 `状态`。如果尚未建立项目文档，再显式执行 `初始化`。

在 Claude Code 中可使用 `/progressive-project-design 状态` 等斜杠命令调用；Claude Code 也会根据 Skill 的 `description` 在相关任务中自动加载它。

## 仓库结构

```text
progressive-project-design/
├── SKILL.md                  # Skill 的行为、状态模型和操作协议
├── agents/
│   └── openai.yaml          # Codex 展示名称与默认提示词
└── references/
    ├── migration.md         # 存量文档迁移规则
    └── templates.md         # 渐进式项目文档模板
```

## 许可证

本项目采用 [MIT License](LICENSE)。
