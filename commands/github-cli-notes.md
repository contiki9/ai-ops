---
description: GitHub CLI（gh）利用時の失敗しやすい点と回避策のメモ
---
# GitHub CLI メモ（GitHub CLI notes）

エージェントやスクリプトが `gh` に依存するときの、よくあるつまずきと推奨経路の集約です。挙動は **GitHub 側の API・`gh` のバージョン**で変わり得るため、再現を共有するときは `gh --version` を併記できるとよいです。

## Issue の取得

| 状況 | 推奨 |
|------|------|
| `gh issue view <N>` が GraphQL エラー（Projects classic 廃止メッセージなど）で全体が失敗 | `gh issue view <N> --json title,body,state,labels,url` など、必要フィールドのみ指定。または `gh api` |
| Web の raw URL を認証なしで取得し 404（非公開リポなど） | **`gh issue view` / `gh api`** など認証済み経路を使う |

## Pull Request

| 状況 | 推奨 |
|------|------|
| `gh pr edit` が GraphQL エラー（例: ラベル付与時に classic Projects 関連） | **GitHub Web UI** でラベル・レビューアを設定する、または **`gh api` の REST** で labels 等を更新する |
| PR のメタデータ | `gh pr view <N> --json title,body,state,labels,url` などで必要フィールドを明示 |
| 行コメントや特定のレビュー本文 | `gh api repos/<owner>/<repo>/pulls/<N>/comments` など **REST** で取得する使い分け |

## Issue の本文を編集するとき

長文や特殊文字をシェルに直接渡すと本文が壊れやすいです。**`gh issue edit <N> --body-file <path>`** を使い、本文用の一時ファイルは次のいずれかに置いてください。

- **リポジトリ内**: リポジトリ直下の **`.tmp/` 以下**（`.gitignore` 済みの標準置き場）
- **リポジトリ外**: OS の **`/tmp/`** などワーキングツリー外（誤コミットを避けたいときの代替）

リポジトリ内に置く場合は **`.tmp/` 以外のパスに下書きを置かない**ようにすると、コミット漏れ・混入のリスクを減らせます。

## MCP と `gh` のフォールバック

MCP の GitHub ツールが使えない環境（ディスクリプタが無い、サーバ未接続など）では、**`gh` 前提の手順**をドキュメントに残しておくと再現性が上がります。

## 関連コマンド定義

- Issue 作成・閲覧の流れ: `commands/create-issue.md`
- PR 作成: `commands/create-pr.md`
