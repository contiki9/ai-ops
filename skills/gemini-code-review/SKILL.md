---
name: gemini-code-review
description: 作業完了後に Gemini CLI の Code Review 拡張（/code-review または /pr-code-review）でコードレビューを依頼する手順を案内します。CLI・拡張のインストールは README を参照してください。
---

# Gemini CLI Code Review Workflow

Use this skill when the user wants a **post-work code review** via **Gemini CLI** with the [Code Review extension](https://github.com/gemini-cli-extensions/code-review) (slash commands `/code-review` and `/pr-code-review`).

## Agent role and limitations

- The **interactive Gemini CLI session runs in the user’s terminal** (or their environment). Do not assume you can drive Gemini CLI on their machine unless they run it themselves or delegate terminal access explicitly.
- Your primary responsibilities: **walk through the steps**, help interpret **pasted** review output, and when you **summarize or relay** findings in this project, follow `.gemini/styleguide.md`.

## Prerequisites (no install steps here)

1. The user has completed environment setup per **README.md**, section **「Gemini CLI と Code Review 拡張」**.
2. Prefer the **repository root** as the working directory when running Gemini CLI for branch-based review.

## Headless (non-interactive) CLI and pitfalls

- **`gemini -p "/code-review"`** (or `-p` with another initial prompt): if the user uses **`--approval-mode plan`**, the CLI may **block shell execution**, so the extension cannot run `git diff` against `origin/HEAD` and the review **aborts**. Use an approval mode that allows the tools the extension needs (e.g. **default** with confirmations, or **`-y` / YOLO** only if the user explicitly accepts that risk).
- For the **code-review extension path**, include the **literal slash command** **`/code-review`** (or **`/pr-code-review`** for PRs). A vague natural-language-only request can behave like a normal agent turn and **not** follow the extension’s dedicated workflow.
- The extension may produce **Japanese prose** in the middle but still close with a **short English summary** (e.g. “No issues found…”). If every line must be Japanese, the in-session styleguide reminder (see below) matters even more.

## Branch changes: `/code-review`

1. **Sanity check**: Ask the user to confirm they are on the **intended branch** and that the repo state matches what they want reviewed (e.g. current branch name, `git status`). You do not need to document the extension’s internal diff rules.
2. Open a terminal at the target repository root (the project whose diff should be reviewed).
3. Start **Gemini CLI** (interactive session) in that directory.
4. **Language (optional)**: If the review should be **Japanese**, have the user tell Gemini in that session—before or when invoking `/code-review`—to follow `.gemini/styleguide.md` (Japanese, desu/masu, brief rationale for suggestions). Extension defaults may not match that automatically.
5. Run the slash command **`/code-review`** so the extension analyzes changes on the current branch.

## Pull request: `/pr-code-review`

1. **GitHub MCP** must be enabled in Gemini CLI for PR review. Setup and caveats are documented in **README.md** (same section) and in the [Gemini CLI MCP documentation](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md).
2. In Gemini CLI, either:
   - run **`/pr-code-review`** with the **PR URL** (e.g. `/pr-code-review https://github.com/org/repo/pull/123`), or
   - configure **`REPOSITORY`**, **`PULL_REQUEST_NUMBER`**, and optionally **`ADDITIONAL_CONTEXT`** per the extension’s documentation, then invoke the command as appropriate for the user’s CLI version.
3. **Language (optional)**: Same as branch flow—user can ask Gemini in-session for Japanese output aligned with `.gemini/styleguide.md` if needed.
4. Remind the user that **GitHub authentication and token scopes** depend on their local MCP configuration.

## Review output quality

When **summarizing, relaying, or acting on** Gemini’s review output inside this project (including text the user pastes from Gemini CLI), align with `.gemini/styleguide.md` at the repository root: **Japanese**, **desu/masu**, professional tone, and **brief rationale** for any change suggestions.

## Usage trigger

Invoke when the user asks for a code review **after finishing work** using **Gemini CLI** and the **code-review** extension (branch or PR), or when they ask how to run that review flow.
