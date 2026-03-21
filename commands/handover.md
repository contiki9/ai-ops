---
description: 現在のセッション状態を引き継ぎ書（HANDOVER.md）として出力します
---

# Create Session Handover (HANDOVER.md)

Summarize the current session state and create a handover document so work can be seamlessly resumed in the next session.

## Execution Steps

1. **Gather Information**
   - Current branch name and working tree status.
   - Uncommitted changes and diffs against the main branch.
   - Related PR (Pull Request) or Issue information.
   - Progress status from `TODO.md` (if it exists).

2. **Generate HANDOVER.md**
   - Using the gathered information and conversational context, create `HANDOVER.md` in the project root (overwrite if it exists).
   - Use the template below.

## Template

```markdown
# HANDOVER: [Brief Task Title]

**Date**: [YYYY-MM-DD HH:MM]
**Branch**: `[Current Branch Name]`
**PR**: [PR Number/URL, or "Not created"]
**Summary**: [1-2 sentences summarizing what was done in this session]

---

## 1. Current State & Changes
- **Uncommitted Changes**: [Yes/No]
- **Key Modified Files**: 
  - `[File path]` - [Role or what changed]

---

## 2. Objective & Context
[Purpose of the task, including Issue references in a few lines]

---

## 3. Completed & Pending Tasks

### Completed
- [x] [Completed task]

### Pending (Next steps)
- [ ] **[Highest priority task]**
- [ ] [Next task]

---

## 4. Key Decisions & Notes
- **[Decision]**: [Reasoning or context]
- **⚠️ Note**: [Gotchas or things to avoid in the next session]

---

## 5. Commands & Resources
\`\`\`bash
# Command to run first
[Command]
\`\`\`
- [Related URLs or files]
```

## Guidelines

- The handover document is a "map", not a "diary". It should help the next session resume work immediately.
- Emphasize "what to do next" and "why decisions were made" over simply listing completed tasks.
- Notify the user once the document has been completely generated.
