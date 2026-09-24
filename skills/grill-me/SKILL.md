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

→ <your recommended answer>

---

**Q2** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

→ <your recommended answer>
```

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

Structure schedules the questions; substance comes from what you probe. Across the session, cover each of these dimensions at least once, weighted toward wherever the plan is thinnest:

- **Hidden assumptions** — unstated beliefs the plan rests on; what "everyone knows" but nobody has said.
- **Success criteria** — how you'll know it worked, in measurable terms.
- **Failure modes** — what breaks, how likely, how badly, and what happens then.
- **Scope boundaries** — what is explicitly in, out, and deferred; non-goals count too.
- **Trade-offs & alternatives** — what else could work, and why this option wins.
- **Reversibility** — can the decision be undone cheaply, or is it a one-way door?
- **Dependencies & constraints** — other decisions, systems, people, or deadlines this presupposes.

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), look it up yourself — or dispatch a sub-agent to find it when delegation is available and authorized. Don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Do not act on it until the user confirms you have reached a shared understanding.
