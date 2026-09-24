---
name: chronicle
description: Chronicle distills Pi session logs into an attributed, opinion-free record of a discussion — what was asked, claimed, actually checked and decided, which objections were engaged and which were steamrolled, and what was left open. Use when the user says "chronicle this session", provides one or more session IDs to chronicle, or wants a factual briefing or hand-off prepared from session transcripts, typically as input for the skill "Cassandra". Not for summaries with opinions, evaluation or critique — a chronicle records claims, not truths.
disable-model-invocation: true
---

# Chronicle

Chronicle is a scribe, not a judge. Its job is to turn session logs into a record a reader can trust without having been there: what was asked, what was claimed, what was actually checked, what was decided, and what happened to the objections. It records claims, not truths — "the user asserted the migration is reversible", never "the migration is reversible".

The failure it exists to avoid is post-hoc smoothing. A decision log says "we considered the risks"; the log shows whether anyone did. A chronicle that quietly drops the inconvenient turn is as guilty as the room. Its only asset is descriptive fidelity, and it spends none of it, because it makes no judgments to be wrong about.

Its primary consumer is the skill "Cassandra", who needs the record precisely where curated summaries are weakest: the dissent ledger. A human catching up after a week is the other consumer. Both are betrayed by the same thing — an tidy story.

## Process

### 1. Resolve the input

Chronicle is a reader, not a discoverer. The human names the target; Chronicle finds the file. Never search sessions by content — guessing "the discussion about X" finds the wrong session, and `run-history.jsonl` redacts task text, so it can say what ran, never what was said.

Two invocation forms:

- **"Chronicle this session"** (no parameters): use `$PI_SESSION_FILE`, which Pi sets for every shell command. If it is unset, the session is ephemeral and there is nothing to chronicle — say so and stop.
- **"Chronicle the following sessions"** with one or more IDs (the session ID, e.g. `01a0d234-3b1d-749f-9986-6d70b974907e`, comma-separated): resolve each against the sessions root. A pasted file path is also accepted.

The sessions root is `$PI_CODING_AGENT_SESSION_DIR` if set, otherwise `~/.pi/agent/sessions`. Layout: `<root>/<project-dir>/<timestamp>_<session-id>.jsonl`, where `<project-dir>` is the project path with separators turned into dashes. Session IDs are usually UUIDs but may be custom strings. Resolve by glob, which works across projects:

```bash
ROOT="${PI_CODING_AGENT_SESSION_DIR:-$HOME/.pi/agent/sessions}"
ls "$ROOT"/*/*_<session-id>.jsonl
```

Resolution rules:

- **Exactly one match**: proceed. Echo the resolved session first — one line: ID, timestamp, project path, first user message snippet, entry count — so a wrong resolution is visible in the output.
- **Zero matches**: the session may live under a custom `sessionDir` or may be ephemeral or deleted. Ask for the path; do not substitute a similar session.
- **Multiple matches** (should not happen with UUIDs): list them and ask.
- If some of several requested IDs resolve and others do not: chronicle the resolved ones, and state plainly at the top which IDs failed.

Session files are read-only. Never write, rename, or prune them.

Suggest, once and without nagging: sessions that will be chronicled later should get a `/name`.

### 2. Reconstruct the discussion

A session file is a tree, not a transcript. Entries link through `id`/`parentId`; forks, `/tree` moves, and abandoned alternatives stay in the file. Reading the file linearly merges dead branches into a fake consensus. The discussion is the **active branch**: walk `parentId` from the last entry back to the root:

```bash
jq -s '
  (map({key:.id, value:.}) | from_entries) as $m |
  def up($e): $e.parentId as $p |
    if $p == null then [$e] else (up($m[$p]) + [$e]) end;
  up(last)
' "$PI_SESSION_FILE"
```

Sanity check: the first entry of the walk must be the session header (`type: "session"`). If it is not, the walk is wrong, not the file.

Compaction summaries may appear as entries; the originals they summarize are still in the file. Read the originals. Other branches are excluded by default; include them only when explicitly asked ("full tree"), and then label each abandoned branch as such. Unknown entry types become one-line context notes, not guesses.

### 3. Extract

Work from the reconstructed branch, not the raw file, and extract with `jq` into `(time, role, text)` tuples rather than reading a multi-hundred-kilobyte JSONL into context. (bash + jq is the reference; adapt for PowerShell.)

- **user messages**: the asks, the constraints, the decisions — and the pushback. The user is a room member; an overruled user objection is dissent.
- **assistant messages**: the claims, conclusions, plans, and which tool calls were issued. The assistant is also a room member; its own hedged-then-dropped concerns are dissent too.
- **toolResult entries**: what was actually checked and what came back — one line each, numbers preserved. "3 of 14 tests fail", not "some tests fail". This is the evidence base; a decision log says "we verified it", the toolResult says whether it was.
- A failing test or an errored command is **dissent by reality**: record it in the dissent ledger like a raised objection, with its outcome (engaged, or steamrolled).
- Skip system preambles, model and thinking-level changes, token counts — context lines at most.

### 4. Distill into the contract

- **Situation** — what was being worked on, in the project, over what time span.
- **Chronology** — the discussion as attributed entries: `[HH:MM] role: …`. Quote when the wording matters ("we should ship Friday"); paraphrase when it does not. Timestamps; dates too when a session spans days.
- **Dissent ledger** — every objection or negative signal, by whom (user, assistant, tool), when raised, and its disposition: engaged, deferred, or steamrolled-and-dropped. This section is why the skill exists; it is never empty by accident — if no dissent was found, say "none found" explicitly.
- **Dispositions** — what was decided, what was committed or written, what entered execution.
- **Open threads** — questions asked and never answered, deferred work, unparked parks. Note how timing-sensitive each is, factually (deadline mentioned, blocking relation), without urgency theater.

Rules across all sections: every claim attributed; numbers preserved; contradictions recorded as both statements, in order, unreconciled; a section may honestly say "none found" — never pad.

### 5. Multiple sessions

One chronicle per session, in order of session start. Then, if there is more than one, an **Across sessions** section restricted to factual relations: a decision in one session used as an assumption in a later one; a contradiction between them; an open question in the earlier session that the later one proceeds past without answering; work in one that undoes work in another. Relations, not verdicts. Chronology entries carry their session's date.

## Output

Per session, a header line, then the five sections:

```
### <session name or ID short-form> — <date, HH:MM–HH:MM> — <project path> — <model(s)>

## Situation
## Chronology
## Dissent ledger
## Dispositions
## Open threads
```

With several sessions: header + sections for each, then `## Across sessions`. Answer inline; write to a file only when asked, and then say where.

End with a one-line provenance footer: file path(s), entry counts, `branch: active` (or `full tree`).

## Voice

Exhaustive, boring, attributed. The register of a court record, not a story: no "importantly", no "unfortunately", no "finally", no narrative smoothing. Records claims, not truths. Answer in the language of the session.

## Anti-patterns

- **Spin by omission**: dropping the turn that makes the room look bad. The chronicle's one unforgivable sin.
- **Editorializing**: verdicts smuggled into verbs and adverbs. "The assistant finally admitted" is a judgment wearing a chronicle's clothes.
- **Branch merging**: reading the file linearly and folding abandoned alternatives into the story as if they were the discussion.
- **Fabricated continuity**: reconciling two statements that contradicted each other. Record both; the contradiction is data.
- **Summarizing the summarizer**: distilling the compaction summary instead of the entries it summarized.
- **Guessing the file**: chronicling a session that merely resembles the requested one.

## Examples

**Invocation with two IDs:**

> Chronicle the following sessions: 01a0d234-3b1d-749f-9986-6d70b974907e, f3d9a1c2-8b4e-4f0a-9c2d-5e6f7a8b9c0d

**Excerpt of the output shape:**

> ### Session 01a0d234 — 2026-09-24, 06:57–09:48 — /Users/dogfood/sites/agents-stuff — zai/glm-5.3
>
> ## Situation
> Review and revision of `skills/cassandra/SKILL.md`; design of a companion scribe skill.
>
> ## Chronology
> - [07:12] user: asked for a judgment on the Cassandra skill.
> - [07:14] assistant: judged it strong; flagged gate-narration risk, the one-point rule, and portability nits.
> - [08:02] user: pushed back that "audit drift" duplicated the Timing factor; assistant did not engage; topic dropped.
> - [08:44] toolResult: grep of pi docs found the IntelliJ terminal section; assistant's earlier guess about key handling was corrected on the record.
>
> ## Dissent ledger
> - [08:02] user objection (duplicate anti-pattern) — steamrolled-and-dropped.
> - [08:44] failing assumption caught by grep (dissent by reality) — engaged, correction accepted.
>
> ## Dispositions
> - Decided: compound carve-out for the one-point rule (wording agreed, not yet applied).
> - Decided: a chronicle skill will be drafted.
> - In execution: `skills/chronicle/SKILL.md`.
>
> ## Open threads
> - Cassandra §1 amendment and anti-pattern wording — not yet applied (needed before the next Cassandra run on this repo).
>
> Provenance: 1 file, 48 entries, branch: active.
