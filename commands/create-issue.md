---
description: GitHub Issueを作成する
---
# Create Issue

## Overview

Create a clear GitHub Issue from the user's request.
Investigate related code first, draft the Issue, get user approval, then create
it with `gh issue create`.

## Steps

1. **Confirm request**
    - Collect problem/proposal details from the user
    - Ask follow-up questions only when required info is missing
2. **Select issue type**
    - Bug/defect: use bug-style sections
    - Feature/proposal: use proposal-style sections
    - If `.github/ISSUE_TEMPLATE/` exists, follow the closest template
3. **Investigate current implementation**
    - Search related files and existing behavior
    - Identify likely cause (for bugs) or impact/approach (for proposals)
    - Check for duplicate implementation (same feature, function, endpoint)
4. **Plan fix or approach**
    - Define concrete resolution policy
    - List implementation tasks and done criteria
5. **Draft issue**
    - **Bug template**
      - 概要
      - 再現手順
      - 修正しないとどう困るか
      - 原因と思われる部分
      - 修正案 / 理想と思われる状況
      - 備考
    - **Proposal template**
      - 概要/背景
      - 対応方針
      - 完了条件
      - 備考
6. **User review**
    - Show title/body draft to user
    - Reflect requested edits, then wait for explicit Go sign
7. **Create issue**
    - Use `gh issue create` after approval
    - Preserve line breaks safely (HEREDOC or file-based body)
    - Return the created Issue URL from command output

## Command Example

```bash
gh issue create --title "タイトル" --body "$(cat <<'EOF'
本文
EOF
)"
```
