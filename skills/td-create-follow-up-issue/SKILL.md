---
name: td-create-follow-up-issue
description: Evaluate whether new TD issues should be created, based on the logged information on a TD issue
---

On a TD issue (see `td-task-management`) (if no issue ID has been provided, look at the issues that are currently in review), the implementer and reviewer have
recorded observations beginning with "Possible new issue:". Evaluate them.

For each logged observation, in order:

1. **Verify it is real.** Do not create an issue from a described risk you have not confirmed against the code. If the log says a future change could break something, check whether the coupling it describes actually exists.
2. **Ask what observably breaks** if it is never done - a failing test, a wrong output, a user-visible defect, a documented contract that stops holding. Speculative, stylistic, symmetry, and "not yet covered" observations do not pass. Neither does an environment failure the project does not have; check before assuming a CI, a shallow clone, or a second consumer exists.
3. **Ask whether it self-surfaces.** If the next change in that area would trip a test, the type checker, or lint, no issue is needed.
4. **Ask which documented goal it advances.** Name it from `.docs/` or `.plans/`. If the answer is "general quality" or "consistency", it stays a log.
5. **Check whether it belongs to an existing open issue.** If an open issue's scope would close this observation anyway, log it there and stop. Two issues closed by one change should never both exist.

Only an observation that passes all five becomes an issue.

Constraints on what you create:

- At most one issue per invocation, regardless of how many logs qualify. If two
  qualify, create the one with the larger consequence and log the other with a
  note that it was deferred deliberately.
- P2 or higher. P3 follow-ups are not created here.
- Description and acceptance criteria are proportionate to the work. A two-point chore does not get eight acceptance criteria. If the criteria are longer than the change will be, the issue is over-specified.
- Acceptance criteria state observable outcomes, not an implementation you have already chosen.
- English, and assumptions documented.

Close by reporting what you decided **and what you declined**: list the observations that stayed logs and the question each one failed. It lets the next session see that the observation was considered and rejected, so it is not raised a third time.
