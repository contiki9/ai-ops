---
description: GitHub Issueを作成する
---
# Issue の作成（Create Issue）

## 概要（Overview）

ユーザーの依頼から、再現性のある GitHub Issue を作成する。関連コードと既存テンプレートを先に確認し、案を作成してユーザー承認を得てから `gh issue create` で作成する。

**成果物について**: Issue の**タイトルと本文**は、特に指示がない限り**日本語**で書く。コマンド例や CLI のプレースホルダは英語のままでよい。

## 手順（Steps）

1. **依頼内容の確認（Confirm request）**
    - 問題の内容、背景、期待する結果をユーザーから整理する
    - 不足している情報があるときだけ追加で質問する
    - 要件や完了条件が曖昧な場合は、`skills/grill-me` の方針（1問ずつ深掘り、推奨回答案を併記、コードベースで答えられる点は先に調査）で先に要件を収束させる
2. **Issue 種別の選択（Select issue type）**
    - 必ず `.github/ISSUE_TEMPLATE/` 配下のテンプレートを確認する
    - バグ・不具合: `bug_report.md` を優先する
    - 機能提案・その他: `issue_template.md` を優先する
    - テンプレにない項目を足す場合は最小限にし、理由を説明する
3. **現状実装の調査（Investigate current implementation）**
    - 関連ファイルと現在の挙動を確認する
    - バグなら想定原因を、提案なら影響と方針を整理する
    - 重複実装（同一機能・関数・エンドポイント）がないか確認する
4. **修正方針・アプローチの整理（Plan fix or approach）**
    - 具体的な修正方針または実装方針を定義する
    - 実装タスクと完了条件を明確にする
5. **ドラフト作成（Draft issue）**
    - **バグテンプレート（`bug_report.md`）**
      - 概要
      - 再現手順
      - 未修正時の影響
      - 想定原因
      - 修正案・あるべき挙動
      - メモ・懸念
    - **標準テンプレート（`issue_template.md`）**
      - 概要・背景（必須）
      - 対応方針
      - 完了条件
      - メモ・懸念
6. **ユーザー確認（User review）**
    - タイトル・本文の案をユーザーに共有する
    - 修正依頼を反映し、明示的な承認があるまで待つ
7. **Issue 作成（Create issue）**
    - 承認後にのみ `gh issue create` を実行する
    - 改行を安全に保つため HEREDOC やファイル経由で body を渡す。本文ファイルをリポジトリ内に置く場合は **`.tmp/` 以下**に置く（`commands/github-cli-notes.md` 参照）
    - コマンド出力から作成された Issue の URL を返す

## コマンド例（Command Example）

`--body` に HEREDOC を渡すか、`--body-file` でファイルを指定する。

### HEREDOC を使う場合

```bash
gh issue create --title "Title" --body "$(cat <<'EOF'
Body
EOF
)"
```

### 本文ファイルを使う場合

```bash
gh issue create --title "Title" --body-file .tmp/issue-body.md
```

## GitHub CLI: Issue の閲覧（トラブルシュート）

自動化やエージェントが Issue の内容を取得するときは、**`--json` で必要フィールドを明示**してください。デフォルト表示（`gh issue view <issue_number>` のみ）は Projects (classic) 関連の GraphQL 非推奨で失敗しやすいため、実行手順には含めません。

```bash
gh issue view <issue_number> --json title,body,state,labels,url
# リポジトリを明示する例
gh issue view <issue_number> --repo <owner>/<repo> --json title,body,state,labels,url
# `gh issue view` が失敗する場合のフォールバック（REST）
gh api repos/<owner>/<repo>/issues/<issue_number>
```

非公開リポジトリでは、認証なしの HTTP フェッチが 404 になることがあるため、**認証済みの `gh`** または `gh api` を使ってください。共通の注意事項（`gh pr view` / `gh pr edit`、本文の安全な編集、PR コメントの REST 取得など）は `commands/github-cli-notes.md` を一次参照としてください。
