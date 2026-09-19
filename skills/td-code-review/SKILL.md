---
name: td-code-review
description: Conduct a code review of the TD issues pending review as part of the TD workflow.
---
I want a code review with the "td - Task Management for AI Agents" workflow (**critical**: you must know the content of `td-task-management`). There are issues waiting for a review.

See [td-implementation-standards.md](../td-shared/td-implementation-standards.md) for the implementation standards in TD-workflows.

If you deem it useful, spawn **cold** subagents. Never fork the current conversation. Give the subagents a defined scope (to avoid scope creep):

- _Codebase Explorer_ for code/docs. Reads specifically the affected files, neighboring code, and docs/plan, reports only evidenced risks
- _Test Reviewer_ for coverage. Checks acceptance criteria against tests, edge cases, regressions, and whether the correct check was run.
- _Integration Reviewer_: only for larger tickets; looks at persistence/API/UI/runner chaining and possible side effects
- **You** integrate and decide.

## When issues arise

Assess whether the issues you find are purely theoretical. If you have no evidence for these issues, then ignore the theoretical issues.

If you find issues, you are free to "reject" the issue. If you assess the implementation as sufficient, you can give an approval.


## Possible Follow-Up Issues

Anything you notice outside the issue scope is recorded with `td log` on the reviewed issue, beginning with "Possible new issue:"

Is it a follow-up issue? Proposing an issue is the exception. Before you propose one, answer all three in
the log entry itself:

1. **Consequence** - what observably breaks, and for whom, if this is never done? Name the failing test, the wrong output, the user-visible defect.  
   "A future change could ...", "this is inconsistent with ...", and "this is not covered" are not consequences.
2. **Self-surfacing** - would this show up on its own the next time someone touches this area, through a failing test, a type error, or lint? If yes, the codebase is already the reminder. Log only.
3. **Goal** - which goal in `.docs/` does this advance? Name it. If the honest answer is "general quality", log only.

If any answer is weak, it is a log, not an issue.

Hard limits:

- At most one proposed issue per review. If you have two candidates, the second one is a log. Choosing costs you nothing and is itself useful signal.
- No proposed issue below P2. If it is not worth a P2, it is worth a log.
- No follow-up may target the code or tests written by the issue under review. Hardening the hardening is an infinite regress: no assertion is so strict that a careful reader cannot propose a stricter one. Strictness is declared by the maintainer, never by the reviewer, and never by the next review in the chain.
- If the same area has produced a follow-up in each of the last two reviews, do not propose a third. Log it and state in the log that the chain is being stopped deliberately.

Then apply the skill `td-create-follow-up-issue <issue-id>`.

