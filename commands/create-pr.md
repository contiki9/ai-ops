---
description: プルリクエストを作成する
---
# プルリクエストの作成 (Create PR)

## 概要 (Overview)

適切に構成された説明文、ラベル、レビュアーを含むプルリクエスト（PR）を作成する。
PR を作成する前に、`commands/git-commit.md` に従ってコミットが作成されていることを確認すること。
PR の本文は `.github/PULL_REQUEST_TEMPLATE.md` に基づいて作成する必要がある。

**注意**: 既存の PR の説明文を更新する場合は、`commands/generate-pr-description.md` を使用すること。

## 手順 (Steps)

1. **ブランチの準備 (Prepare branch)**
    - すべての変更がコミットされていることを確認する。
    - `commands/git-commit.md` に従ってコミットメッセージを作成する。
    - ブランチをリモートにプッシュする。
    - ブランチが main に対して最新であることを確認する。
2. **Issue の確認 (Verify Issue)**
    - PR に紐づく Issue がある場合、`gh issue view <issue_number> --json title,body,state,labels,url`（またはユーザー指定の URL）で内容を取得し、今回の変更内容・スコープと一致するかを確認する。デフォルト表示が GraphQL エラーで失敗する場合の扱いは `commands/github-cli-notes.md` を参照する。
    - **完了条件（受け入れ基準）**を読み、実装・PR 説明で満たせているか、不足がないかを確認する。
    - チャット上のユーザー指示と Issue の記述が食い違う場合は、ユーザーの明示指示を優先する。
    - 不足や曖昧さがある場合は、ユーザーに続行方針を確認し、合意が得られるまで PR 作成は行わず中断する。
    - 紐づく Issue がない場合はこのステップをスキップする。
3. **PR 説明文の作成 (Write PR description)**
    - `.github/PULL_REQUEST_TEMPLATE.md` を基本構造として使用する。
    - 各セクションをプロジェクト固有の具体的な詳細で埋める。
    - セクションが該当しない場合は、明示的に「該当なし」と記載する。
    - UI の変更が含まれる場合はスクリーンショットを追加する。
    - 説明文をファイルに下書きする場合は **`.tmp/` 以下**に置く（コミットに含めないため。詳細は `commands/github-cli-notes.md`）。
4. **PR のセットアップ (Set up PR)**
    - 記述的な **日本語のタイトル** で PR を作成する（英語タイトルは使わない）。
    - 適切なラベルを追加する。
    - レビュアーを割り当てる。
    - 関連する Issue をリンクする。
    - `gh pr edit` やラベル付与で GraphQL エラー（Projects classic 関連など）が出る場合は、Web UI または `gh api`（REST）での更新を検討する（詳細は `commands/github-cli-notes.md`）。

## PR テンプレート (PR Template)

- **タイトルの言語**: プルリクエストのタイトルは**日本語**で書く。
- 参照: `.github/PULL_REQUEST_TEMPLATE.md`
- 少なくとも以下を含めること:
  - `# 概要/対応issue`
  - `# 変更内容`
  - `# テストの観点`
  - `# 影響範囲`
  - `# 動作要件`
  - `# 補足`
