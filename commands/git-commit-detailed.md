---
description: コミットメッセージ詳細版を作成するワークフロー
---

# Create Detailed Commit Message Workflow

This workflow generates a commit message based on the current changes according to a specified format, and presents it for the user to copy.
**※ This workflow does NOT automatically execute the commit. The user must review the message and commit manually.**

## Execution Steps

1. **Understand the Changes**
   - Read and understand the currently staged changes and the scope of work.

2. **Generate the Commit Message**
   - Select the appropriate prefix based on the work (`feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, or `chore`).
   - Create a brief summary text of the changes.
   - Insert **two blank lines (newlines)** after the summary.
   - Describe the detailed changes as a bulleted list using hyphens (`-`).
   - If an associated Issue number is known, add it at the very end after a newline, formatted like `#123`.

3. **Branch Safety Check (when actually committing)**
   - Run `git branch --show-current` and check the current branch.
   - If the branch is `main` or `master`, do **not** commit directly on that branch.
   - Derive a new branch name from the commit content and create/switch to it before committing.
     - Format:
       - With Issue key: `<type>/<issue-key>-<short-summary-slug>`
       - Without Issue key: `<type>/<short-summary-slug>`
     - **GitHub Issue number (default when known):** If a primary GitHub Issue is known (URL, chat, or description), **include `#<number>` in the branch name at least once** by default. For multiple issues, use the single primary issue the user or PR identifies. Omit the number when there is no corresponding issue.
     - Examples: `feat/PROJ-123-add-profile-image`, `feat/#45-add-image-upload`, `fix/#12-handle-token-refresh`, `fix/handle-token-refresh` (no issue)
     - **Shell and #:** In bash/zsh, # starts a comment unless quoted. Always **quote** branch names that contain '#', e.g. `git switch -c 'feat/#21-add-login'`.
   - Create and switch: `git switch -c '<new-branch-name>'` (quote when the name includes `#`)
   - After switching, run commit on the new branch.

4. **Present the Commit Message**
   - Output the generated commit message **ONLY within a Markdown code block** so the user can copy and paste it directly. Do not include any extra commentary inside the code block.

---

### Output Format Example

When presenting to the user, output it in a code block like below:

```text
feat: Add profile image upload feature

- Create a new component to allow users to upload images
- Add error handling for images exceeding 5MB in size
- Add image saving logic to the API endpoint

#45
```
