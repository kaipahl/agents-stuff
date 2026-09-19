# Critical: Communication in TD

Use `td log <issue-id>` (for TD work sessions: `td ws log`) during work with the appropriate flags for relevant progress, decisions, and observations (decision, blocker, hypothesis, tried, result). Don't just log "started" or "done", but specifically:
- which files/modules you have changed
- which tests/checks you have run and with what result
- which acceptance criteria are fulfilled
- which deliberate limitations, open points, or deviations from the plan exist

Every Communication and every text in TD **must be in english**.

## Communication before review

If an acceptance criterion is not fulfilled or you are unsure, do not submit the issue for review, but document the remaining point.

The `td handoff` before review must be reviewer-ready:
- `--done`: specifically what has been implemented
- `--remaining`: nothing / or specific remaining points
- `--decision`: important architecture or tooling decisions
- `--uncertain`: uncertainties, risks, unverified assumptions
- Never use generic handoffs like "Auto-generated for review submission".
- If you found possible improvements outside the scope of the issue, record them with `td log <issue-id>`, one per improvement, beginning with "Possible new issue:".
- A log is an observation that is preserved where the next reader of this issue will find it, without adding a board item that someone has to carry, triage, and eventually close.
- Write the log so it is decidable later without re-reading the diff: what you observed, what would observably break if it is never addressed, and whether it would surface on its own through an existing test, type check, or lint rule.
- Do not propose a priority, points, or acceptance criteria in the log. Proposing them frames the observation as a ticket-in-waiting and pre-commits the later evaluation to creating one.
- "I noticed X but it has no observable consequence" is a valuable log entry. Write it. Do not inflate it into a defect to justify having noticed it.
