---
name: commit
description: Draft a git commit message (subject + body) for the currently staged changes, following the house convention `<type>(scope) <issue-id>: <title>`.
disable-model-invocation: true
---

# Commit Message

Write a commit message for the staged changes. If you don't have questions about
the commit message, you can run `git commit` yourself.

## Format

```
<type>(<scope>)[!] <issue-id>: <title>
                                                    ← blank line
<body: why this change was made>
                                                    ← blank line
[footers]
```

Example:

```
fix(auth) ABC-123: Refresh token before expiry instead of after

Users were logged out mid-session because the refresh only fired after
the API had already rejected the expired token. Refreshing 60s ahead
removes the race between the request and the expiry check.
```

## Rules

### Subject line

- Maximum **72 characters**, counted over the entire line.
- `type` — **required**. Exactly one of the types below, lowercase.
- `scope` — **required**. Lowercase, kebab-case, one word or short noun
  naming the affected area (module, package, directory, feature). Derive
  it from the changed paths. If the change spans several areas, choose
  the dominant one — or suggest splitting the commit.
- `!` — directly after `)` if the change is breaking (see Footers).
- `issue-id` — the ticket ID (e.g. `ABC-123`, `#42`). Look for it in the
  branch name first (`git branch --show-current`). If there is no ticket,
  use the literal `no-ticket`. Never invent an ID. Ask the user if he didn't
  gave you the information in the prompt.
- `title` — English, imperative mood ("Add", not "Added"/"Adds"),
  capitalized first word, no trailing period. It completes the sentence
  "If applied, this commit will …".

### Types

| Type       | Use for                                                       |
| ---------- | ------------------------------------------------------------- |
| `feat`     | A new feature for the user                                    |
| `fix`      | A bug fix for the user                                        |
| `docs`     | Documentation only                                            |
| `style`    | Formatting, whitespace, semicolons — no change in behavior    |
| `refactor` | Code change that neither fixes a bug nor adds a feature       |
| `perf`     | Code change that improves performance                         |
| `test`     | Adding or correcting tests                                    |
| `build`    | Build system or external dependencies (npm, composer, vite …) |
| `ci`       | CI configuration and scripts                                  |
| `chore`    | Maintenance that touches neither src nor tests                |
| `revert`   | Reverts a previous commit                                     |

No other types are allowed.

### Body

- Separated from the subject by **exactly one blank line**.
- Every line **hard-wrapped at 72 characters** or less. No soft wrap.
- English.
- Explain **why**, not **what**. The diff already shows what changed.
  Answer: What problem existed? Why this solution? What constraint or
  trade-off drove the decision? What is the impact?
- Do not list changed files or narrate the diff line by line.
- A body may be omitted only for trivial changes where the subject is
  self-explanatory (typo fixes, dependency bumps without reason to note).

### Footers

- Separated from the body by one blank line, `Token: value` format,
  each line ≤ 72 characters.
- Breaking change: add `!` to the subject **and** a footer
  `BREAKING CHANGE: <what breaks and how to migrate>`.
- `revert`: add `Refs: <sha>` of the reverted commit and explain in the
  body why it is reverted.

## Workflow

1. Run `git diff --staged` (and `git diff --staged --stat` for overview).
   If nothing is staged, stop and tell the user.
2. If the staged changes mix unrelated concerns, recommend splitting them
   and name the proposed commits before drafting anything.
3. Determine type, scope, and issue ID. If the *why* is not inferable from
   the diff, the branch name, or the conversation, **ask** — do not
   fabricate motivation.
4. Draft the message.
5. Verify the length limits mechanically before presenting:

   ```bash
   awk 'length > 72 { print "Line " NR " too long (" length "): " $0 }' msg.txt
   ```

   and confirm line 2 is empty. Fix and re-check until clean.
