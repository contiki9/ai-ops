---
description: コミットを作成する
---
# Git Create Commit

## Overview

Create a short, focused commit message and commit staged changes.

## Steps

1. **Review changes**
    - Check the diff: `git diff --cached` (if changes are staged) or `git diff` (if unstaged)
    - Understand what changed and why
2. **Ask for issue key (optional)**
    - Check the branch name for an issue key (Linear, Jira, GitHub issue, etc.)
    - If an issue key (e.g., POW-123, PROJ-456, #123) is not already available in the chat or commit context, optionally ask the user if they want to include one
    - This is optional - commits can be made without an issue key
3. **Stage changes (if not already staged)**
    - `git add -A`
4. **Branch safety check**
    - Run `git branch --show-current` and check the current branch
    - If the branch is `main` or `master`, do **not** commit directly on that branch
    - Create and switch to a new branch based on the commit content before committing
    - Branch naming rule:
      - With Issue number: `<type>/#<issue-number>-<short-summary-slug>`
      - Without Issue number: `<type>/<short-summary-slug>`
    - Example: `feat/#00-example-example`, `feat/#45-add-profile-image-upload`, `fix/handle-token-refresh`
    - Create and switch: `git switch -c <new-branch-name>`
5. **Create short commit message**
    - Base the message on the actual changes in the diff
    - Example: `git commit -m "fix(auth): handle expired token refresh"`
    - Example with issue key: `git commit -m "PROJ-123: fix(auth): handle expired token refresh"`

## Template

- `git commit -m "<type>(<scope>): <short summary>"`
- With issue key: `git commit -m "<issue-key>: <type>(<scope>): <short summary>"`

## Rules

- **Length:** <= 72 characters
- **Imperative mood:** Use "fix", "add", "update" (not "fixed", "added", "updated")
- **Capitalize:** First letter of summary should be capitalized
- **No period:** Don't end the subject line with a period
- **Describe why:** Not just what - "fix stuff" is meaningless
