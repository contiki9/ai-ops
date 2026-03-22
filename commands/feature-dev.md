---
description: 新機能・新規要望向けの構造化開発ワークフロー（発見から実装・レビューまで）
---
# Feature Dev

## Overview

Guide feature and new-requirement work in a structured, multi-phase workflow: understand the ask, explore the codebase, remove ambiguity, compare architecture options, implement only after explicit approval, review quality, and summarize outcomes.

Inspired by systematic feature-development workflows; adapted to be **tool-agnostic** (use search, reading, and todos instead of vendor-specific agents).

**Use for:**

- New features that span multiple files or layers
- Requirements that need architectural or integration decisions
- Work where ambiguity (edge cases, errors, compatibility) must be resolved before design

**Do not use for:**

- One-line fixes, trivial changes, or urgent hotfixes
- Fully specified, very small tasks

For lightweight branch and setup steps, see `setup-new-feature.md`. For clarification-only passes, use `clarify-task.md` (e.g. in Phase 3).

## Steps

1. **Discovery**
    - Restate the feature or request; identify the problem being solved
    - Capture constraints, non-goals, and acceptance criteria at a high level
    - Summarize your understanding and confirm with the user before exploring deeply

2. **Codebase exploration**
    - Search and read code for similar features, patterns, and integration points
    - Map relevant architecture (layers, modules, data flow, entry points)
    - List candidate files and extension points; note risks of duplicating existing behavior
    - Present a concise findings summary (key paths, patterns, recommended touch points)

3. **Clarifying questions**
    - From findings and the request, list underspecified areas: edge cases, error handling, integrations, backward compatibility, performance, security, and UX expectations where relevant
    - Organize questions clearly; **wait for user answers before proceeding** to architecture design
    - When helpful, follow the multiple-choice style in `clarify-task.md` to speed alignment

4. **Architecture design**
    - Propose **at least two or three** approaches (e.g. minimal change, cleaner separation, pragmatic balance)
    - For each: scope, main components, trade-offs, and fit with existing patterns
    - Give a recommendation with rationale; **wait for the user to choose** (or approve a variant) before implementation

5. **Implementation**
    - **Start only after explicit user approval** of the chosen approach
    - Re-read relevant files; implement following project conventions and prior exploration
    - Avoid scope creep and unrelated refactors; track progress with todos where appropriate
    - Respect project rules (e.g. no unapproved UI/UX changes, no unapproved dependency/version bumps)

6. **Quality review**
    - Review from multiple angles in parallel (as separate passes): simplicity/DRY, correctness/bugs, conventions/abstractions
    - Report issues with severity; cite file and line references where possible
    - **Ask the user** whether to fix now, defer, or proceed as-is; act on their choice

7. **Summary**
    - Describe what was built, key decisions, and files touched
    - Suggest next steps (tests, docs, rollout, follow-up features)

## Feature Dev Checklist

- [ ] Restated the request and confirmed understanding (Discovery)
- [ ] Explored the codebase and summarized findings (Exploration)
- [ ] Asked clarifying questions and **received answers** before design (Phase 3 gate)
- [ ] Presented multiple architecture options and trade-offs (Architecture)
- [ ] **User selected or approved** an approach before coding (Phase 4–5 gate)
- [ ] Implemented only in-scope changes per approved design (Implementation)
- [ ] Ran a structured quality review and **user decided** on fixes (Phase 6 gate)
- [ ] Delivered a final summary with decisions and suggested next steps (Summary)
