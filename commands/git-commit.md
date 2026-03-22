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
      - With Issue key: `<type>/<issue-key>-<short-summary-slug>`
      - Without Issue key: `<type>/<short-summary-slug>`
    - **GitHub Issue number (default when known):** If a primary GitHub Issue is known (from the issue URL, chat, or description), **include `#<number>` in the branch name at least once**—this is the expected default, not optional polish. If work spans multiple issues, use the single primary issue the user or PR calls out. Skip the number when there is no corresponding issue (small maintenance, emergency patch, internal-only changes, etc.).
    - Examples: `feat/PROJ-123-add-profile-image`, `feat/#45-add-image-upload`, `fix/#12-handle-token-refresh`, `fix/handle-token-refresh` (no issue)
    - **Shell and `#`:** In bash/zsh, `#` starts a comment unless quoted. Always **quote** branch names that contain `#`, e.g. `git switch -c 'feat/#21-add-login'`.
    - Create and switch: `git switch -c '<new-branch-name>'` (use quotes when the name includes `#`)
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
