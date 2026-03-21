---
description: プルリクエストを作成する
---
# Create PR

## Overview

Create a well-structured pull request with proper description, labels, and
reviewers.
Before creating the PR, ensure commits are created by following
`commands/git-commit.md`.
The PR body must be created based on `.github/PULL_REQUEST_TEMPLATE.md`.

## Steps

1. **Prepare branch**
    - Ensure all changes are committed
    - Create commit messages by following `commands/git-commit.md`
    - Push branch to remote
    - Verify branch is up to date with main
2. **Write PR description**
    - Use `.github/PULL_REQUEST_TEMPLATE.md` as the base structure
    - Fill each section with concrete project-specific details
    - If a section is not applicable, explicitly write that it is not applicable
    - Add screenshots when UI changes are included
3. **Set up PR**
    - Create PR with descriptive title
    - Add appropriate labels
    - Assign reviewers
    - Link related issues

## PR Template

- Reference: `.github/PULL_REQUEST_TEMPLATE.md`
- Include at least:
  - `# 概要/対応issue`
  - `# 変更内容`
  - `# 影響範囲`
  - `# 動作要件`
  - `# 補足`
