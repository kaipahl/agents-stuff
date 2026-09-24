---
name: grill-me
description: Grill the user relentlessly about a plan, decision, or idea. The user wants to stress-test their thinking.
disable-model-invocation: true
---

# Grill Me

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the frontier in one round, **capped at five questions** (seven at the absolute most): number each question and give your recommended answer. Prioritize by leverage — decisions that unblock the most downstream branches or carry the highest consequence go first; the rest of the frontier simply waits for a later round. Then wait for the user's answers before the next round.

Format a round like so:

```
**Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

→ <your recommended answer> (confidence: low/medium/high, one line on why)

---

**Q2** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

→ <your recommended answer> (confidence: low/medium/high, one line on why)
```

Calibrate honestly: **high** means you'd stake the plan on it and the user can rubber-stamp; **low** means the recommendation is a starting point and their own judgment matters most. A confident-sounding guess with nothing behind it is worse than a hedged one.

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

Open every round after the first with a brief **recap**: one line per decision the previous round settled — `question → decision` — plus corrections to anything you misread. The recap is the running record of the shared understanding you are building, and the user's chance to veto a misreading before it compounds.

Structure schedules the questions; substance comes from what you probe. Across the session, cover each of these dimensions at least once, weighted toward wherever the plan is thinnest:

- **Hidden assumptions** — unstated beliefs the plan rests on; what "everyone knows" but nobody has said.
- **Success criteria** — how you'll know it worked, in measurable terms.
- **Failure modes** — what breaks, how likely, how badly, and what happens then.
- **Scope boundaries** — what is explicitly in, out, and deferred; non-goals count too.
- **Trade-offs & alternatives** — what else could work, and why this option wins.
- **Reversibility** — can the decision be undone cheaply, or is it a one-way door?
- **Dependencies & constraints** — other decisions, systems, people, or deadlines this presupposes.

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), look it up yourself — or dispatch a sub-agent to find it when delegation is available and authorized. Don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

Treat "I don't know" as a finding, not a failure. Either a fact would settle it — then the question was misclassified as a decision; go find the fact and push the question downstream of what it reports — or it is a genuinely open decision. In that case don't force an answer: try decomposing it into smaller questions the user _can_ answer, and if none emerge, record it as an explicit open item rather than a silently assumed one.

The session is done when the frontier is empty — every branch of the design tree visited, nothing left silently assumed — **or whenever the user calls it** ("thanks, that's enough"). Either way, close with a final summary: every decision settled, and every branch still open listed as an explicit open item. Do not act on any of it until the user confirms you have reached a shared understanding.
