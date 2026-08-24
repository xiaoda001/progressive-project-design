# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

AI コーディングエージェント向けの漸進的プロジェクト設計 Skill です。Just-in-Time Design、垂直スライス、コードと文書のキャリブレーションにより、継続的に変化するプロジェクトを明確かつ実行可能に保ち、過剰な先行設計を防ぎます。

## 用途

大規模な先行文書は実装開始後に陳腐化しやすく、エージェントへ不要なコンテキストを与えます。この Skill は、現在の意思決定と垂直スライスに必要な情報だけを準備し、コード、テスト、設定、実行結果を根拠に文書を校正します。

- 新規プロジェクトに軽量で発展可能なアーキテクチャ文書を導入する
- 既存の ADR、RFC、文書規約を維持したまま既存プロジェクトを移行する
- 要件を観測・検証可能なエンドツーエンドのスライスへ分割する
- 最小で安全な次のタスクを特定し、一度に一つ進める
- 実装と設計文書のずれを検出する
- 完了したスライスをアーカイブし、日常コンテキストを削減する

## 主な機能

### 短いアクションによるワークフロー

| アクション | 目的 |
|---|---|
| `status` / `状態` | プロジェクト、文書、現在のスライス、ずれ、証拠を読み取り専用で確認 |
| `init` / `初始化` | 最小限の漸進的文書構造を作成または移行 |
| `requirement` / `需求` | 観測可能な成果を明確化し、要件を分類 |
| `change` / `变更` | スライス、インターフェース、データ、依存関係への影響を分析 |
| `plan` / `规划` | 次の垂直スライスを計画 |
| `prepare [Sx]` / `准备 [Sx]` | 指定スライスを実装可能な状態へ準備 |
| `next` / `下一步` | 現在の証拠から最小の実装タスクを決定 |
| `go` / `推进` | 安全でブロックされていない最小タスクを一つ実装・検証 |
| `calibrate [Sx]` / `校准 [Sx]` | 実装証拠に基づいて文書を更新 |
| `archive [Sx]` / `归档 [Sx]` | 完了条件を検証し、履歴資料をアーカイブ |

### 3 次元の状態モデル

- 文書成熟度：`D0`（登録）から `D4`（実装との校正済み）
- 設計深度：`L0`（境界）から `L2`（必要な非機能制約）
- スライス実行状態：`planned`、`ready`、`in-progress`、`blocked`、`calibrating`、`done`

`D4` はコード、テスト、設定、マイグレーション、実行可能な入口を確認した後にのみ設定します。完了したスライスはコールドアーカイブへ移し、履歴が実際に必要な場合だけ読み込みます。

## 利点

- 現在のスライスに必要な L1 情報だけを準備し、過剰設計を抑制
- 完了履歴をコールドアーカイブへ移してコンテキストを削減
- 実装と検証証拠により文書のずれを管理
- 要件変更を分類してからスコープを変更し、進行中の作業を保護
- 既存の README、ADR、RFC、ロードマップ、モジュール文書に適応
- 読み取り専用分析、文書更新、コード実装の権限を分離

## インストール

リポジトリのルートが完全な [Agent Skills](https://agentskills.io/) ディレクトリです。`SKILL.md` が共通入口で、`references/` は必要時のみ読み込まれます。

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

インストール後に Agent を再起動するか、Skill 検出を更新してください。更新方法：

```bash
git -C <skill-directory>/progressive-project-design pull --ff-only
```

## 使用例

```text
$progressive-project-design status
$progressive-project-design init
$progressive-project-design requirement チーム招待機能を追加
$progressive-project-design prepare S1
$progressive-project-design go
$progressive-project-design calibrate S1
$progressive-project-design archive S1
```

既存プロジェクトでは最初に `status` を実行してください。Claude Code では `/progressive-project-design status` で呼び出せます。

## リポジトリ構成

```text
progressive-project-design/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── migration.md
    └── templates.md
```

## ライセンス

[MIT License](LICENSE)
