---
name: create-command
description: ユーザーの要件に基づいて新しいCommands（Markdownファイル）を作成します。
---

# Create AI-Ops Command

This skill enables the agent to automatically create and deploy a new AI-Ops command (as a Markdown file) within the `commands/` directory, based on the user's requirements.

## Guidelines for Command Creation

1. **Location and Format**
   - Place the new command file inside the `commands/` directory.
   - Use the `.md` extension.
   - The file must begin with YAML frontmatter containing a concise `description` (written in Japanese).

2. **Command Structure and Style**
   - **Prompt-Based**: Write the command instructions as clear prompts for an AI agent to execute. Avoid relying on complex, obscure Bash scripts.
   - **Simplicity**: Ensure the instructions are straightforward, easy for both humans and AI to understand, and executable step-by-step.
   - **Language**: The core logic, templates, and outputs of the command should be formulated in Japanese by default, adhering to the project's global rules (`AGENTS.md`) unless the user specifies otherwise. Keep the AI instructions within the file clear (which can be in English or Japanese depending on the context, but follow the style of existing commands).

3. **Checklist Before Finalizing**
   - Confirm that the command file contains the necessary YAML metadata.
   - Ensure the instructions focus on "what to do" rather than just giving a terminal script to run.
   - After creation, ask the user if they would like to add the new command to the `README.md` command list.

## Usage Trigger

Invoke this skill when the user explicitly requests to create or add a new workflow, command, or AI-Ops instruction file (e.g., "Create a command to format code", "Add a new AI-ops workflow for deployment").
