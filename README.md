# AI-Ops

AI に依存する現代の開発プロセスを効率化するための、AI エージェント・コマンド・スキルのコレクションリポジトリです。本リポジトリは **Cursor**, **Antigravity**, **Claude Code** などの複数の AI ツールで汎用的に利用できるように設計されています。

## 特徴
- **ツールの非依存化**: Cursor や Claude といった特定ツールに依存せず、すべての AI アシスタントに共通の指示・ワークフローを提供します。
- **日本語中心のワークフロー**: 利用頻度の高い `commands/` の本文は日本語で読めるよう整備しており、`AGENTS.md` の言語方針と揃えています（CLI や慣習的な英語表記は維持します）。
- **カテゴリ別の整理**: コード品質、Git 操作、テスト、ドキュメントなど、目的別にコマンドが整理されています（物理配置は `commands/` 直下。迷いやすい重複の整理方針は [`docs/command-consolidation-policy.md`](docs/command-consolidation-policy.md) を参照）。
- **バージョン管理**: 今後追加されるカスタムワークフローやスキルはすべて本リポジトリで管理します。

## ディレクトリ構成
- `commands/` : AI エージェントに渡すプロンプトやワークフローの Markdown ファイル集。
- `skills/` : エージェント向けの補助スキル。各サブディレクトリに `SKILL.md` があります。
  - **`create-command`**: 新しい `commands/` 用 Markdown コマンドを追加するときの指針。
  - **`gemini-code-review`**: 作業完了後に Gemini CLI の Code Review 拡張（`/code-review` / `/pr-code-review`）でレビューするときの運用（セットアップは下文「Gemini CLI と Code Review 拡張」）。
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

## Gemini CLI と Code Review 拡張

作業ブランチや PR に対して [Gemini CLI Code Review extension](https://github.com/gemini-cli-extensions/code-review) でレビューを取りたい場合のセットアップです。実際のレビュー手順（`/code-review` / `/pr-code-review`）はエージェント向けスキル [`skills/gemini-code-review/SKILL.md`](skills/gemini-code-review/SKILL.md) にまとめています（インストール手順は本節のみに記載します）。

### Gemini CLI

- 未導入の場合は [Gemini CLI のインストール手順](https://github.com/google-gemini/gemini-cli?tab=readme-ov-file#-installation)に従ってください。
- Code Review 拡張を使うには **Gemini CLI v0.4.0 以上**が必要です（拡張 README の要件）。バージョンは `gemini --version` などで確認してください。

### Code Review 拡張のインストール

ターミナルで次を実行します。

```bash
gemini extensions install https://github.com/gemini-cli-extensions/code-review
```

### PR をレビューする場合（GitHub MCP）

`/pr-code-review` を使うには Gemini CLI 側で [GitHub MCP サーバー](https://github.com/github/github-mcp-server) を有効にする必要があります。設定の詳細は [Gemini CLI の MCP ドキュメント](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md)を参照してください。

拡張の README では、PR レビュー時に次のいずれかが使えるとされています。

- **`/pr-code-review <PR の URL>`** で PR を指定する
- 環境変数 **`REPOSITORY`**（リポジトリ）、**`PULL_REQUEST_NUMBER`**（PR 番号）、任意で **`ADDITIONAL_CONTEXT`**（フォーカスしたい文脈）を設定する

**注意**: GitHub への認証方法・トークンのスコープ・ネットワーク環境は利用者ごとに異なります。MCP 経由でリポジトリにアクセスできない場合は、ローカル設定と GitHub MCP のドキュメントを確認してください。

### レビュー結果のスタイル

Gemini への共通トーンや PR 説明のルールはリポジトリルートの [`.gemini/styleguide.md`](https://github.com/contiki9/ai-ops/blob/main/.gemini/styleguide.md) を参照してください（日本語・ですます調など）。ローカルでは同パスのファイルを開けます。

## コマンドの探し方

- **整理方針・重複の扱い（Lint / Security / 図解 / PR など）**: [`docs/command-consolidation-policy.md`](docs/command-consolidation-policy.md)（Issue #8 の合意ベースライン）
- **実体**: すべて [`commands/`](commands/) 直下の Markdown。ツールによってはこのディレクトリをそのままリンクまたはコピーする

## コマンド一覧（全件）

`commands/` は物理的にフラット配置です。下表のカテゴリは**主目的に基づく論理分類**であり、ディレクトリ構造とは一致しません。責務の整理・重複の扱いは [`docs/command-consolidation-policy.md`](docs/command-consolidation-policy.md) を参照してください。各コマンドの説明は対応する Markdown の frontmatter `description` と同一です（ファイル名は昇順）。

### 機能開発・タスク整理

| コマンド名 | 説明 |
|------------|------|
| `clarify-task.md` | タスクの内容を明確化・整理する |
| `feature-dev.md` | 新機能・新規要望向けの構造化開発ワークフロー（発見から実装・レビューまで） |
| `roadmap.md` | 開発ロードマップを作成・更新する |
| `setup-new-feature.md` | 新機能実装に向けた要件や準備をまとめる |

### Lint・コード品質

| コマンド名 | 説明 |
|------------|------|
| `deslop.md` | コードの無駄を省きクリーンアップする |
| `lint-fix.md` | リンターのエラーを修正する |
| `lint-suite.md` | プロジェクト全体のリンターを実行し、修正してクリーンにする |
| `refactor-code.md` | コードのリファクタリングを実施する |

### テスト・ビルド・デバッグ

| コマンド名 | 説明 |
|------------|------|
| `debug-issue.md` | バグや問題をデバッグする |
| `fix-compile-errors.md` | コンパイルエラーを修正する |
| `run-all-tests-and-fix.md` | 全テストを実行し、エラー箇所を修正する |
| `write-unit-tests.md` | 単体テストを作成する |

### レビュー

| コマンド名 | 説明 |
|------------|------|
| `code-review.md` | コードレビューを実施する |
| `light-review-existing-diffs.md` | 既存の差分を軽くレビューする |

### GitHub・Issue・PR

| コマンド名 | 説明 |
|------------|------|
| `address-github-pr-comments.md` | PRのレビューコメントに対応する |
| `create-issue.md` | GitHub Issueを作成する |
| `create-pr.md` | プルリクエストを作成する |
| `generate-pr-description.md` | プルリクエストの詳細を最新のものに更新する |
| `github-cli-notes.md` | GitHub CLI（gh）利用時の失敗しやすい点と回避策のメモ |

### Git 操作

| コマンド名 | 説明 |
|------------|------|
| `fix-git-issues.md` | Gitのコンフリクトや問題を解決する |
| `git-commit-detailed.md` | コミットメッセージ詳細版を作成するワークフロー |
| `git-commit.md` | コミットを作成する |
| `git-push.md` | 変更をリモートへプッシュする |

### セキュリティ

| コマンド名 | 説明 |
|------------|------|
| `security-audit.md` | セキュリティ監査を実施する |
| `security-review.md` | コードのセキュリティレビューを実施する |

### 図解・可視化

| コマンド名 | 説明 |
|------------|------|
| `diagrams.md` | アーキテクチャやフローの図解を作成する |
| `overview.md` | プロジェクトの全体概要を記述する |
| `visualize.md` | （非推奨）図解は diagrams.md を使用してください |

### ドキュメント・オンボーディング

| コマンド名 | 説明 |
|------------|------|
| `add-documentation.md` | ドキュメントを追加・更新する |
| `generate-api-docs.md` | APIドキュメントを生成する |
| `onboard-new-developer.md` | 新規参画者向けのオンボーディングガイドを作成する |

### 運用・品質横断・インフラ

| コマンド名 | 説明 |
|------------|------|
| `accessibility-audit.md` | アクセシビリティの監査を実施する |
| `add-error-handling.md` | エラーハンドリングを追加する |
| `database-migration.md` | データベースのマイグレーションを実行する |
| `docker-logs.md` | Dockerのログを確認・分析する |
| `handover.md` | 現在のセッション状態を引き継ぎ書（HANDOVER.md）として出力します |
| `optimize-performance.md` | コードのパフォーマンスを最適化する |

## ライセンスについて
本リポジトリの元となるコマンド群は、`hamzafer/cursor-commands` のコードをベースとして取り込み、独自の再編を行ったものです。オリジナルコードのライセンスおよび帰属については `THIRD_PARTY_LICENSES.md` を参照してください。

このリポジトリ全体の運用については `LICENSE` (MIT License - Copyright 2026 contiki9) に従います。
