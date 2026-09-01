# Critical: Communication in TD

Use `td log <issue-id>` (for TD work sessions: `td ws log`) during work with the appropriate flags for relevant progress, decisions, and observations (decision, blocker, hypothesis, tried, result). Don't just log "started" or "done", but specifically:
- which files/modules you have changed
- which tests/checks you have run and with what result
- which acceptance criteria are fulfilled
- which deliberate limitations, open points, or deviations from the plan exist

## Communication before review

If an acceptance criterion is not fulfilled or you are unsure, do not submit the issue for review, but document the remaining point.

The `td handoff` before review must be reviewer-ready:
- `--done`: specifically what has been implemented
- `--remaining`: nothing / or specific remaining points
- `--decision`: important architecture or tooling decisions
- `--uncertain`: uncertainties, risks, unverified assumptions
- Never use generic handoffs like "Auto-generated for review submission".
- If you have found possible improvements outside the scope of the issue (e.g. performance improvement, possible refactoring, architecture improvement)
  - For each possible improvement, one `td log <issue-id>` each.
  - The log message begins with "Possible new issue:"
  - This is followed by your decision template for later evaluation of whether a new issue should be created.
