---
description: プルリクエストの詳細を最新のものに更新する
---
# Generate PR Description

## Overview

Compare the current pull request (PR) description with the actual commits and code diffs to generate an updated description.
This workflow focuses on filling in missing implementation details, correcting inconsistencies, and supplementing missing test or impact information to ensure a smooth review process.

## Operational Prerequisites

- The existing PR description must be accessible (e.g., via `gh pr view`).
- The current branch must reflect the latest code changes or commit history.
- The output of this command is a "proposal"; always review the content before applying it to the PR.

## Reference Template

- Use the project's PR template as the base for the output: `.github/PULL_REQUEST_TEMPLATE.md`

## Steps

1. **Information Gathering**
    - Retrieve the current PR body (Description).
    - Review all commit messages on the target branch and the diff against the base branch (e.g., `main`).
2. **Analysis and Extraction**
    - Compare the implementation with the PR description and extract items for update based on:
        - **Omissions**: Implemented features or changes not mentioned in the PR body.
        - **Inconsistencies**: Descriptions in the PR body that do not match the actual code changes or are outdated.
        - **Missing Details**: Lack of testing results, impact areas, operational requirements, or supplemental info (e.g., screenshots).
3. **Generate Update Proposal**
    - Create an updated PR body in Japanese while maintaining the structure of the template specified in "Reference Template".
    - Organize by sections as needed to make changes clear.
4. **Final Review**
    - Verify that the generated content does not contain excessive summarization or misinterpretations.
    - Output in a format that can be directly pasted into the PR body.

## Checkpoints

- [ ] Are all major implemented changes included in the "変更内容" (Changes) section?
- [ ] Have old specifications that were deleted or changed been removed from the PR body?
- [ ] Are the specific details of tests performed (unit tests, manual verification, etc.) documented?
- [ ] Is the impact on other features (影響範囲) thoroughly considered?
- [ ] Are environment variables or configuration changes (動作要件) clearly stated?
- [ ] Are notes for reviewers or supplemental information up to date?

## Output Format

Follow the template structure from `.github/PULL_REQUEST_TEMPLATE.md` and output all items in Japanese.
Ensure that the output includes all sections defined in the template (e.g., 概要/対応issue, 変更内容, テストの観点, 影響範囲, 動作要件, 補足).
