# Progressive Project Design

[简体中文](README.md) | [English](README.en.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

AI コーディングエージェント向けの漸進的プロジェクト設計 Skill です。Just-in-Time Design、垂直スライス、コード↔文書の校正を組み合わせ、過剰な先行設計を避けながら文書を実装とともに進化させます。

## 基本原則

> 文書は意思決定の出発点ではなく、意思決定の成果物です。

- 現在の判断またはスライスに必要な内容だけを設計する
- 実行・検証可能な最小のエンドツーエンドスライスを単位にする
- 現在の成果物が完成したら止め、後続範囲を先に設計しない
- コード、テスト、設定、実行結果を使って文書を校正する
- モジュール文書にコード位置、依存関係、バックリンクを記録する

## 状態モデル

| 次元 | 状態 |
|---|---|
| 文書成熟度 | `D0` 登録 → `D1` 草案 → `D2` 実装可能 → `D3` 実装中 → `D4` 校正済み |
| 設計深度 | `L0` 境界 → `L1` 現在のスライスに必要 → `L2` 必要な詳細を完全化 |

通常は L1 で実装を開始し、現在の実装が例外処理や性能などを本当に必要とする場合だけ L2 に進みます。

## 文書体系

Skill は `.ppd/` を唯一の漸進的文書入口として使用します。

```text
.ppd/
├── README.md
├── 01-overview/
├── 02-architecture/
├── 03-plan/
├── 04-progress/<slice>/
└── 05-modules/
```

既存プロジェクトでは、現在のコードからモジュール、インターフェース、データモデル、依存関係を抽出し、一つのスライスずつ逆向きに校正します。

## 5 段階のリズム

| 段階 | きっかけ | 成果物 |
|---|---|---|
| 骨格 | プロジェクト初期化 | `.ppd/README.md` と最小ディレクトリ |
| 要件 | 境界確認後 | 位置づけ、範囲、判断、非目標 |
| スライス開始 | 実装準備時 | 必要な技術選択、モジュール L1、ロードマップ |
| 実装中 | 意味のある変更 | 短いログ、判断理由、残課題 |
| 校正 | スライス完了 | D3→D4、コード位置、差異、バックリンク |

## インストール

リポジトリのルートが完全な [Agent Skills](https://agentskills.io/) ディレクトリです。

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

更新：

```bash
git -C <agent-skill-directory>/progressive-project-design pull --ff-only
```

## 使用例

```text
$progressive-project-design このプロジェクトの漸進的設計状態と最小の次の作業を確認してください
$progressive-project-design 新規プロジェクト用の最小 .ppd 骨格を作成してください
$progressive-project-design 現在のロードマップから次の垂直スライスを計画してください
$progressive-project-design 現在のスライスに関係するモジュール文書を校正してください
```

Claude Code では `/progressive-project-design 現在の状態を確認してください` のように呼び出します。

## リポジトリ構成

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

## ライセンス

[MIT License](LICENSE)
