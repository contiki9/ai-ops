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

## コマンド一覧（一部）
- `feature/` : `feature-dev.md`, `setup-new-feature.md`, `clarify-task.md` など
- `code-quality/` : `lint-fix.md`, `refactor-code.md`, `deslop.md` など
- `documentation/` : `generate-api-docs.md`, `onboard-new-developer.md` など
- `git/` : `code-review.md`, `create-pr.md`, `git-commit.md`, `git-commit-detailed.md` など
- `testing/` : `run-all-tests-and-fix.md`, `debug-issue.md` など
- `security/` : `security-audit.md` など

## ライセンスについて
本リポジトリの元となるコマンド群は、`hamzafer/cursor-commands` のコードをベースとして取り込み、独自の再編を行ったものです。オリジナルコードのライセンスおよび帰属については `THIRD_PARTY_LICENSES.md` を参照してください。

このリポジトリ全体の運用については `LICENSE` (MIT License - Copyright 2026 contiki9) に従います。
