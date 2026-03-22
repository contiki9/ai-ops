# コマンド重複整理方針（Issue #8）

本ドキュメントは [`commands/`](../commands/) 配下ワークフローの**責務の再定義**と、重複・統合・非推奨の**合意ベースライン**を示す。実装の段階的な統合やファイル削除は、別 PR で本表に沿って実施する。

## 原則

1. **単一目的**: 1 コマンドは 1 つの主目的（例: 新規 PR 作成、既存 PR 本文の更新）に寄せる。
2. **名称の維持**: 利用実績のあるファイル名は可能な限り残し、統合時は本文で誘導する。
3. **互換**: 削除する場合は README と関連コマンド本文に移行先を明記してから行う（いきなり削除しない）。
4. **除外**: `git-commit-detailed.md` は Issue 指示により**本整理の統合対象外**（現状維持）。

## 重複判定一覧と採用方針

| グループ | 対象ファイル | 重複・混同の理由 | 採用方針（合意） |
|----------|--------------|------------------|------------------|
| Lint | `lint-suite.md`, `lint-fix.md` | いずれも「リンターで直してクリーンにする」に読み取れる。`lint-suite.md` の見出しが `lint-fix` と同趣旨だった。 | **両方存続**し、責務を分離する。**`lint-suite.md`**: プロジェクト（リポジトリ）単位で lint を実行し、オートフィックスと再実行まで含む。**`lint-fix.md`**: ユーザーが指定したファイル／範囲に対する lint 修正に特化。迷ったらリポ全体は `lint-suite`、局所は `lint-fix`。 |
| Security | `security-audit.md`, `security-review.md` | いずれも依存関係・コード・設定のセキュリティを扱う。 | **両方存続**。**`security-audit.md`**: 監査観点（依存の脆弱性、シークレット、設定）のチェックリストと是正の流れ。**`security-review.md`**: コードパスに沿ったレビューと、指摘ごとの修復例・手順。先に広く洗うなら audit、変更コードの深掘りなら review。 |
| 図解 | `diagrams.md`, `visualize.md`, `overview.md` | いずれも Mermaid 等による可視化。`visualize.md` は内容が極薄で `diagrams.md` と主目的が重なる。`overview.md` は製品俯瞰用の固定 TODO・テンプレに近い。 | **`diagrams.md` 存続**（汎用の図解手順）。**`overview.md` 存続**（プロダクト全体の俯瞰図 2 枚に特化）。**`visualize.md` は非推奨**（後方互換のためファイルは残し、冒頭で `diagrams.md` へ誘導）。将来的に本文を `diagrams.md` へ統合して削除してよい。 |
| レビュー | `code-review.md`, `light-review-existing-diffs.md` | いずれも差分・品質のレビュー。 | **両方存続**。**`light-review-existing-diffs.md`**: 速読・リスク箇所の洗い出し・フォローアップ記録。**`code-review.md`**: 承認前の本レビュー（機能・品質・セキュリティ）。 |
| PR 周辺 | `create-pr.md`, `generate-pr-description.md`, `address-github-pr-comments.md` | いずれも PR に関係するが、手順の入口が異なる。 | **3 つとも存続**（統合しない）。新規作成 / 本文更新 / レビューコメント対応は別目的。既に相互参照あり。 |
| 品質改善 | `deslop.md`, `refactor-code.md` | いずれもコードをきれいにする。 | **両方存続**。**`deslop.md`**: AI 生成由来のノイズ（過剰コメント、不要な防御等）の削除に限定。**`refactor-code.md`**: 一般的なリファクタ（構造・性能・保守性）。 |
| 機能開発系 | `setup-new-feature.md`, `feature-dev.md`, `clarify-task.md` | 要件整理や開発フローで隣接。 | **3 つとも存続**。`feature-dev.md` が総合フロー、`setup-new-feature.md` が準備チェック、`clarify-task.md` が質問による要件明確化。`feature-dev.md` 内の参照で役割が分かれている。 |

## 区分サマリー

| 区分 | ファイル例 |
|------|------------|
| **統合候補（将来）** | `visualize.md` → `diagrams.md` への統合を推奨。実施タイミングは別 PR。 |
| **存続（責務を文書で明確化）** | `lint-suite.md` / `lint-fix.md`、`security-audit.md` / `security-review.md`、`diagrams.md` / `overview.md`、`code-review.md` / `light-review-existing-diffs.md`、PR 3 ファイル、`deslop.md` / `refactor-code.md`、機能開発 3 ファイル など。 |
| **現状維持（対象外）** | `git-commit-detailed.md`（Issue 明示）。 |
| **非推奨（ファイル残置）** | `visualize.md`（上記）。 |

## 重複・不要コマンドの扱い（合意）

| 扱い | 条件 |
|------|------|
| **削除** | README・他コマンドからの参照がなく、非推奨期間を経た後に実施。 |
| **統合** | 主目的が同一で、片方にセクション追加で十分な場合。統合後は削除側にリダイレクト用 1 行ファイルを残すか README に記載。 |
| **非推奨** | 互換のためファイルを残し、YAML `description` または本文先頭に移行先を記載（本ポリシーで `visualize.md` を該当とする）。 |

## フォローアップ（別 PR 推奨）

- `visualize.md` の本文を `diagrams.md` に吸収し、ファイル削除またはスタブのみにする。
- `commands/` をカテゴリサブディレクトリに移す場合は、シンボリックリンクまたはツール別マッピング文書が必要（本リポジトリの README の「カテゴリ」表記との整合）。
- 英語のみのコマンドの日本語化は別 Issue で一括扱うとよい。

## 参照

- Issue: https://github.com/contiki9/ai-ops/issues/8
- コマンド実体: [`commands/`](../commands/)
