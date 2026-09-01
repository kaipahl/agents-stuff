---
name: td-implementation
description: Implement issues of the TD board
---
**Critical**: you must know the content of `td-task-management` and follow the TD-workflow.

For TD implementation standards see [td-implementation-standards.md](../td-shared/td-implementation-standards.md)

Work **only** on {all issues of the open TD Work Session | the mentioned TD issue}. **Do not add or work on any additional issues.**

1. Analyze: Read all information and acceptance criteria in the specified TD issue.
2. Explore: If the issue spans multiple files or the scope is unclear, deploy a small subagent (e.g., the Explore subagent using "Haiku") for codebase exploration before writing code.
3. Initialize: Start the implementation by running `td start <issue-id>`
4. Test-Driven Development: Evaluate if additional tests are required by TDD. If yes, implement these tests before changing any production code.
5. Scope: Search ALL call sites and emission sites — do not stop at the first match.
6. Documentation: Update inline docs AND markdown docs to match new semantics
7. Verification (Criteria): Verify explicitly that every acceptance criterion of the issue is fully fulfilled.
8. Verification (Tools): Do linting or type check or other test tools exist? Then run them. **If any command fails, fix the errors and repeat this step before proceeding.**
9. Log: Document your implementation details via `td log <issue-id>`. Communication is a critical part of the implementation (see [td-communication.md](../td-shared/td-communication.md))!
10. Handoff: Hand over with `td handoff`.
11. Submit: Only then submit for review via `td review <issue-id>`. **Critical**: Never close the issue yourself!
