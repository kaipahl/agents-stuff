---
name: td-code-review
description: Conduct a code review of the TD issues pending review as part of the TD workflow.
---
I want a code review with the "td - Task Management for AI Agents" workflow (**critical**: you must know the content of `td-task-management`). There are issues waiting for a review.

See [td-implementation-standards.md](../td-shared/td-implementation-standards.md) for the implementation standards in TD-workflows.

When practical, use subagents for code reviews.

- _Codebase Explorer_ for code/docs. Reads specifically the affected files, neighboring code, and docs/plan, reports only evidenced risks
- _Test Reviewer_ for coverage. Checks acceptance criteria against tests, edge cases, regressions, and whether the correct check was run.
- _Integration Reviewer_: only for larger tickets; looks at persistence/API/UI/runner chaining and possible side effects
- **You** integrate and decide.

## When issues arise

Assess whether the issues you find are purely theoretical. If you have no evidence for these issues, then ignore the theoretical issues.

If you find issues, you are free to "reject" the issue. If you assess the implementation as sufficient, you can give an approval.


## Possible Follow-Up Issues

If, as part of the implementation, you notice possible improvements outside the scope of the issue (performance improvement, possible refactoring, architecture improvement), create a separate `td log` for each possible improvement on the issue. The log message begins with "Possible new issue:" followed by your decision template, so that the project can later evaluate whether a new issue should be created from it.

At the end of the code review, apply the skill `td-create-follow-up-issue <issue-id>`.

