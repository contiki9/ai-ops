---
description: プロジェクト全体のリンターを実行し、修正してクリーンにする
---
# Lint Suite（プロジェクト単位のリンター実行）

## Overview

リポジトリ全体に対してリンターを実行し、自動修正可能なものを適用し、マージ前にフォーマット・スタイル要件を満たすまで繰り返す。**特定ファイルだけ直したい**場合は `lint-fix.md` を使う。

## Steps

1. **Execute linters**
    - Run the standard lint command with autofix enabled if available
    - Capture any remaining errors or warnings from the output
    - Identify files requiring manual attention
2. **Resolve findings**
    - Apply targeted fixes, keeping edits minimal and idiomatic
    - Refactor repeated issues such as unused variables or long functions
    - Update configuration or suppressions only when justified
3. **Verify cleanliness**
    - Re-run the lint command to ensure a zero-issue result
    - Spot-check key files for formatting and readability
    - Stage the changes with clear commit messages when satisfied

## Lint Checklist

- [ ] Linter executed with latest config
- [ ] Autofix results reviewed
- [ ] Manual issues resolved
- [ ] Final lint run passes cleanly
- [ ] Changes staged or ready for PR
