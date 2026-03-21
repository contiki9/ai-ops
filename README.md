# AI-Ops

AI に依存する現代の開発プロセスを効率化するための、AI エージェント・コマンド・スキルのコレクションリポジトリです。本リポジトリは **Cursor**, **Antigravity**, **Claude Code** などの複数の AI ツールで汎用的に利用できるように設計されています。

## 特徴
- **ツールの非依存化**: Cursor や Claude といった特定ツールに依存せず、すべての AI アシスタントに共通の指示・ワークフローを提供します。
- **カテゴリ別の整理**: コード品質、Git 操作、テスト、ドキュメントなど、目的別にコマンドが整理されています。
- **バージョン管理**: 今後追加されるカスタムワークフローやスキルはすべて本リポジトリで管理します。

## ディレクトリ構成
- `commands/` : AI エージェントに渡すプロンプトやワークフローの Markdown ファイル集。
- `skills/` : 今後追加予定のより高度なスクリプトや拡張スキル。
- `AGENTS.md` : AI エージェントがこのリポジトリを扱うための共通ガイドライン。

## 使い方（AI ツール別セットアップ）

### Cursor
Cursor コマンドとして利用するには、プロジェクトの `.cursor/commands` にシンボリックリンクを張るかコピーします。
```bash
# シンボリックリンクの作成例
ln -s /path/to/ai-ops/commands .cursor/commands
```
チャット内で `/` を入力することで、これらのコマンドを呼び出せます。

### Antigravity
Antigravity のワークフローとして利用する場合は、グローバルな設定ディレクトリに配置します。
```bash
cp -r commands/* ~/.gemini/antigravity/workflows/
```
Antigravity のチャット内で `/slash-command` として利用可能になります。

### Claude Code
Claude Code のコマンドやコンテキストとして利用するために、`.claude/commands/` や `CLAUDE.md` へ適用します。

## コマンド一覧
`commands/` 配下に格納されている全てのコマンド一覧です。カテゴリごとに整理しています。

### コード品質 (Code Quality)
| コマンド名（ファイル名） | 説明 |
| :--- | :--- |
| `deslop.md` | コードの無駄を省きクリーンアップする |
| `fix-compile-errors.md` | コンパイルエラーを修正する |
| `lint-fix.md` | リンターのエラーを修正する |
| `lint-suite.md` | リンターの設定と実行を行う |
| `optimize-performance.md` | コードのパフォーマンスを最適化する |
| `refactor-code.md` | コードのリファクタリングを実施する |

### Git・プルリクエスト (Git & Pull Request)
| コマンド名（ファイル名） | 説明 |
| :--- | :--- |
| `address-github-pr-comments.md` | PRのレビューコメントに対応する |
| `code-review.md` | コードレビューを実施する |
| `create-pr.md` | プルリクエストを作成する |
| `fix-git-issues.md` | Gitのコンフリクトや問題を解決する |
| `generate-pr-description.md` | PRの説明文を自動生成する |
| `git-commit-detailed.md` | コミットメッセージ詳細版を作成するワークフロー |
| `git-commit.md` | コミットを作成する |
| `git-push.md` | 変更をリモートへプッシュする |
| `light-review-existing-diffs.md` | 既存の差分を軽くレビューする |

### テスト・デバッグ (Testing & Debugging)
| コマンド名（ファイル名） | 説明 |
| :--- | :--- |
| `add-error-handling.md` | エラーハンドリングを追加する |
| `debug-issue.md` | バグや問題をデバッグする |
| `docker-logs.md` | Dockerのログを確認・分析する |
| `run-all-tests-and-fix.md` | 全テストを実行し、エラー箇所を修正する |
| `write-unit-tests.md` | 単体テストを作成する |

### ドキュメント・設計 (Documentation & Architecture)
| コマンド名（ファイル名） | 説明 |
| :--- | :--- |
| `add-documentation.md` | ドキュメントを追加・更新する |
| `diagrams.md` | アーキテクチャやフローの図解を作成する |
| `generate-api-docs.md` | APIドキュメントを生成する |
| `overview.md` | プロジェクトの全体概要を記述する |
| `visualize.md` | データやフローの可視化を行う |

### セキュリティ・アクセシビリティ (Security & Accessibility)
| コマンド名（ファイル名） | 説明 |
| :--- | :--- |
| `accessibility-audit.md` | アクセシビリティの監査を実施する |
| `security-audit.md` | セキュリティ監査を実施する |
| `security-review.md` | コードのセキュリティレビューを実施する |

### 開発・プロジェクト管理 (Development & Project Management)
| コマンド名（ファイル名） | 説明 |
| :--- | :--- |
| `clarify-task.md` | タスクの内容を明確化・整理する |
| `create-issue.md` | GitHub Issueを作成する |
| `database-migration.md` | データベースのマイグレーションを実行する |
| `handover.md` | 現在のセッション状態を引き継ぎ書（HANDOVER.md）として出力します |
| `onboard-new-developer.md` | 新規参画者向けのオンボーディングガイドを作成する |
| `roadmap.md` | 開発ロードマップを作成・更新する |
| `setup-new-feature.md` | 新機能実装に向けた要件や準備をまとめる |

## ライセンスについて
本リポジトリの元となるコマンド群は、`hamzafer/cursor-commands` のコードをベースとして取り込み、独自の再編を行ったものです。オリジナルコードのライセンスおよび帰属については `THIRD_PARTY_LICENSES.md` を参照してください。

このリポジトリ全体の運用については `LICENSE` (MIT License - Copyright 2026 contiki9) に従います。
