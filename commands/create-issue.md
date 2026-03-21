---
description: GitHub Issueを作成する
---
# Create Issue

## Overview

Create a clear and reproducible GitHub Issue from the user's request.
Review related code and existing templates first, draft the issue, get user approval,
then create it with `gh issue create`.

## Steps

1. **Confirm request**
    - Collect the problem statement, background, and expected outcome from the user
    - Ask follow-up questions only when required information is missing
2. **Select issue type**
    - Always review templates under `.github/ISSUE_TEMPLATE/`
    - Bug/defect: prefer `bug_report.md`
    - Feature/proposal/other: prefer `issue_template.md`
    - If adding fields not in templates, keep changes minimal and explain why
3. **Investigate current implementation**
    - Inspect related files and current behavior
    - For bugs, identify likely causes; for proposals, identify impact and approach
    - Check for duplicate implementation (same feature, function, or endpoint)
4. **Plan fix or approach**
    - Define a concrete fix/implementation policy
    - List implementation tasks and clear done criteria
5. **Draft issue**
    - **Bug template (`bug_report.md`)**
      - Overview
      - Reproduction steps
      - Impact if not fixed
      - Suspected cause
      - Fix proposal / ideal behavior
      - Notes / concerns
    - **Standard template (`issue_template.md`)**
      - Overview / background (required)
      - Approach
      - Done criteria
      - Notes / concerns
6. **User review**
    - Share the issue title/body draft with the user
    - Reflect requested edits, then wait for explicit approval
7. **Create issue**
    - Run `gh issue create` only after approval
    - Preserve line breaks safely via HEREDOC or file-based body
    - Return the created Issue URL from command output

## Command Example

You can pass content using a HEREDOC with `--body`, or use `--body-file`.

### Using HEREDOC
```bash
gh issue create --title "Title" --body "$(cat <<'EOF'
Body
EOF
)"
```

### Using a body file
```bash
gh issue create --title "Title" --body-file ./issue-body.md
```
