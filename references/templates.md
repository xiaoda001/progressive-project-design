# Minimal document templates

Read only the section needed for the artifact being created or updated. Adapt headings to established repository conventions while preserving the required state and evidence fields.

## `docs/README.md`

```markdown
# 项目文档索引

> 原则：按需设计、垂直切片、实现后校准。

## 当前状态

- 当前切片：[S1 / 无]
- 切片状态：[planned / ready / in-progress / blocked / calibrating / done]

## 导航

| 分类 | 文档 | 用途 |
|---|---|---|
| 项目概览 | [01-overview/project-overview.md](01-overview/project-overview.md) | 产品边界和非目标 |
| 技术决策 | [02-architecture/tech-stack.md](02-architecture/tech-stack.md) | 当前切片需要的技术选择 |
| 切片路线图 | [03-plan/roadmap.md](03-plan/roadmap.md) | 切片、验收标准和依赖 |
| 模块索引 | [05-modules/README.md](05-modules/README.md) | 模块 D/L 状态 |
```

Do not link files that do not exist; use `—` until they are created.

## Project overview

```markdown
# 项目概览

> 成熟度：D1
> 设计深度：L0
> 最后校准：—

## 定位

[一句话说明为谁解决什么问题]

## 目标用户与核心路径

- 目标用户：
- 核心路径：

## 部署与数据边界

- 部署形态：
- 数据位置与敏感性：

## 关键决策

| 决策 | 结论 | 依据 | 待确认项 |
|---|---|---|---|

## 明确不做

- [本阶段非目标]
```

## Technology decisions

```markdown
# 技术决策

| 决策 | 选择 | 成熟度 | 适用切片 | 原因 | 重新评估条件 |
|---|---|---|---|---|---|
| [数据库] | [选择] | D1 | S1 | [原因] | [触发条件] |
```

Record only decisions needed by the current or imminent slice. Include exact versions only when compatibility or reproducibility depends on them.

## Slice roadmap

```markdown
# 切片路线图

| ID | 名称 | 状态 | 用户可观察结果 | 验收证据 | 涉及模块 | 依赖/阻塞 | 明确不做 |
|---|---|---|---|---|---|---|---|
| S1 | [名称] | planned | [结果] | [命令、测试或演示步骤] | [模块] | [无/依赖] | [范围外] |

## 当前切片

- ID：S1
- 下一状态条件：[进入 ready / done 所缺的证据]
```

## Module index

```markdown
# 模块索引

| 模块 | 成熟度 | 深度 | 当前切片 | 最后校准 | 文档 |
|---|---|---|---|---|---|
| [模块] | D0 | L0 | — | — | — |
```

## Module document

```markdown
# [模块名称]

> 成熟度：D2
> 设计深度：L1
> 所属切片：S1
> 最后校准：—

## 职责与边界

- 负责：
- 不负责：

## 当前切片流程

[输入 → 关键处理 → 输出]

## 对外接口

| 接口/方法 | 输入 | 输出 | 失败方式 |
|---|---|---|---|

## 数据模型

| 模型 | 必要字段 | 约束 |
|---|---|---|

## 依赖关系

- 依赖：
- 被依赖：

## 验收证据

- [测试、命令或可观察行为]

## 未决问题

- [仅列阻碍当前切片的事项]
```

## Slice log

```markdown
# S1 实现日志

## [日期] [变更标题]

- 变更：
- 原因：
- 影响的接口/数据/范围：
- 验证证据：
- 遗留事项：
```

Append only meaningful entries. Do not create one file per trivial change.

## Calibration entry

Append or update this section in the relevant module document:

```markdown
## 校准记录

| 日期 | 实现证据 | 与原设计的偏差 | 文档调整 |
|---|---|---|---|
| [日期] | [代码、测试、运行结果] | [无/说明] | [调整摘要] |
```

After verification, set maturity to D4 and update `最后校准`.

## Archive index

Create `docs/99-archive/README.md` only when archiving the first slice:

```markdown
# 归档索引

> 冷上下文：日常操作不读取归档正文；仅在当前证据不足且历史相关时按索引逐层检索。

| 切片 | 完成日期 | 用户可观察结果 | 影响模块 | 摘要 |
|---|---|---|---|---|
| S1 | YYYY-MM-DD | [结果] | [模块] | [summary](slices/S1/summary.md) |
```

Keep this index compact. Do not duplicate implementation logs or detailed evidence here.

## Archived slice summary

Create `docs/99-archive/slices/<slice-id>/summary.md` before moving detailed historical artifacts:

```markdown
# S1 归档摘要

- 状态：done / archived
- 完成日期：YYYY-MM-DD
- 用户可观察结果：
- 最终验收证据：
- 影响模块：
- 保留在活跃文档中的当前事实：
- 关键历史决策：
- 已知限制或后续事项：

## 详细历史资料

- [实现日志](implementation-log.md)
```

Link only files that exist. Keep current architectural truth in active documents; use this summary for discovery and historical explanation.
