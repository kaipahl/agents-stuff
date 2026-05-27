---
name: td-fix-rejected-review
description: Address a rejected TD review systematically. Evaluate the rejection and if agreeing, fix the implementation.
---
**Critical**: you must know the content of `td-task-management` and follow the TD-workflow.

For TD implementation standards see [td-implementation-standards.md](../td-shared/td-implementation-standards.md)

1. Read the full rejection comment on the mentioned TD issue
2. Identify root cause category (logic / docs / tests / lint)
3. Evaluate honestly if the rejection was reasonable.
    - If yes: Proceed to step 4.
    - If no: Halt execution, present your counter-argument to the user, and wait for explicit approval to proceed.
4. Start the fix by running `td start <issue-id>`
5. Search ALL call sites / emission sites — do not stop at the first match.
6. Update inline docs AND markdown docs to match new semantics
7. Add a regression test specifically covering the rejection case.
8. Run verification tools: `npm run lint && npm run typecheck && npm test`
9. Ask yourself why the issue was rejected and what could have avoided the rejection. Tell the user.
10. Document your fixes via `td log <issue-id>`. Communication is a critical part of the implementation (see [td-communication.md](../td-shared/td-communication.md))!
11. Hand over with `td handoff`.
12. Only then re-submit via `td review <issue-id>`. **Critical**: Never close the issue yourself!
