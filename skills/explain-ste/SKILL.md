---
name: explain-ste
description: Short, low-jargon explanations of code, technical and scientific topics in a controlled style based on ASD-STE100 Simplified Technical English (STE) — short sentences, one meaning per word, active voice, every technical term defined before use. English and German (follows the user's language). Also simplifies dense technical text.
disable-model-invocation: true
---

# Explain STE

Write technical explanations that a reader can understand on the first read. The base is ASD-STE100 Simplified Technical English (STE), a controlled language from aerospace maintenance documentation. STE was made for readers who are not native speakers and who must not misunderstand an instruction.

## What STE does and what it does not do

STE reduces **linguistic** complexity: ambiguity, synonyms, long sentences, nested clauses. STE does **not** reduce **conceptual** complexity. STE allows technical names ("embedding", "cache", "token") without limits. A text can follow every STE rule and still be full of undefined terms and abstractions.

For this reason, this skill has two layers:

1. **STE writing rules** — how each sentence is built.
2. **Jargon and abstraction rules** — which terms and ideas the reader can handle, and in which order.

Both layers are necessary. Layer 1 without layer 2 gives clean but opaque text. Layer 2 without layer 1 gives friendly but vague text.

## Layer 1: STE writing rules

These rules are a paraphrase of the core STE rules. They are not the complete official specification.

**Words**
- Use one word for one meaning. When you use "file" for a thing, do not later call it "document" or "resource". Synonyms make the reader ask: "Is this a different thing?"
- Give one word only one meaning. Do not use "run" for "execute" and later for "a single test pass".
- Use simple, common verbs: "use", "make", "send", "keep", "show", "start", "stop". Avoid verbs like "leverage", "facilitate", "orchestrate", "utilize".
- Do not make nouns from verbs. Write "the server checks the token", not "the server performs a verification of the token".
- Do not use idioms, metaphors or slang as the main explanation. A comparison is allowed only when you say clearly that it is a comparison (see layer 2).
- Do not use long noun chains. "user session token refresh handler" → "the function that refreshes the token of a user session".

**Sentences**
- Descriptive sentences: maximum 25 words.
- Instruction sentences (procedures, steps): maximum 20 words.
- One idea per sentence. One instruction per sentence.
- Use active voice. Say who does the action: "The browser sends the request", not "The request is sent". Passive voice hides the actor, and the actor is often the most important information in a technical explanation.
- Keep articles and small words ("the", "a", "that"). Do not write in telegram style.
- Write instructions as commands: "Open the file." Not "You should open the file" or "The file is to be opened".
- Put a condition before the action: "If the test fails, read the log." Not "Read the log if the test fails."

**Paragraphs**
- One topic per paragraph.
- Start each paragraph with its main statement. Give details after it.
- Maximum about 6 sentences per paragraph.

## Layer 2: Jargon and abstraction rules

**Rule 1 — Define, then use.** Before you use a technical term for the first time, give a plain definition in one sentence. After that, use the term without change (STE word rule). Do not define terms that the reader clearly knows.

> An **embedding** is a list of numbers that describes the meaning of a text. Texts with a similar meaning get similar lists. The search compares these embeddings.

**Rule 2 — Limit new terms.** Introduce maximum about 3 new technical terms per explanation section. When a topic needs more, split it into steps. Each step teaches one or two terms.

**Rule 3 — Concrete before abstract.** Show a specific example first. Then give the general rule. The reader understands "a dictionary stores `"name": "Kai"`" before "a dictionary is a key-value data structure".

**Rule 4 — Mechanism, not label.** A label is not an explanation. "It uses caching" explains nothing. Say what happens: "The program keeps the last result in memory. When the same question comes again, it uses this result and does not compute it again."

**Rule 5 — Comparisons are marked and limited.** A comparison to daily life can help. Use maximum one per concept. Say clearly where the comparison stops being correct.

**Rule 6 — No unnecessary abstraction words.** Words like "layer", "abstraction", "paradigm", "ecosystem", "framework" (as a general word), "holistic" usually hide the real content. Replace them with the concrete thing.

## German: STE-inspired rules

There is no official German STE and no approved German word list. When the user writes in German, apply the same rules in German, with these additions:

- **Satzlänge:** gleiche Grenzen (20 / 25 Wörter). Deutsche Wörter sind länger — achte deshalb besonders auf Komposita.
- **Komposita auflösen**, wenn sie mehr als zwei Teile haben: „Zugriffsberechtigungsprüfung" → „die Prüfung, ob ein Nutzer Zugriff hat".
- **Verb nach vorn:** Vermeide lange Satzklammern, bei denen das Verb erst am Ende kommt. Teile den Satz lieber.
- **Kein Nominalstil:** „Die Anwendung prüft die Daten", nicht „Es erfolgt eine Überprüfung der Daten durch die Anwendung".
- **Anglizismen:** Ein etablierter englischer Fachbegriff („Token", „Cache") ist erlaubt — mit Definition beim ersten Auftreten. Erfinde keine deutschen Ersatzwörter, die niemand benutzt.
- **Aktiv statt Passiv**, auch bei „werden"-Konstruktionen und „man".
- Duzen oder Siezen: folge dem Nutzer.

## Scope and length

This skill is for code, technical and scientific topics. It gives **short** explanations: the reader wants to understand one thing now, not take a full lesson.

- **Typical length: a few short paragraphs, roughly 250–450 words.** Adjust to the topic: a small question can get a shorter answer, a topic with several moving parts can take more room.
- Focus on the one thing that was asked. Add background or related topics only when they help the reader understand the answer.
- When brevity and the rules pull in different directions, prefer clarity: a slightly longer text with defined terms and simple sentences is better than a short, dense one.

## Structure of an explanation

1. **One-sentence answer.** What is it, or what does it do? In plain words.
2. **Concrete example.** A small, specific case — for code, a few lines or one input/output pair.
3. **How it works.** A few short sentences or numbered steps. Introduce the terms here (rule 1, rule 2).
4. **Limit** (optional, one sentence). Where the simple explanation is not complete.

Use numbered steps for sequences. Use prose for reasons and relations. Do not use bullet lists for things that have a cause-and-effect relation — prose shows the "because".

## Rewriting existing text

When the user gives a text to simplify:

1. Find the technical terms. Decide which ones the reader needs and which ones you can replace.
2. Find the actor in each passive sentence and make it active.
3. Split long sentences.
4. Make all synonyms for one thing into one word.
5. Keep the technical content correct. Simplification must never change the facts. When a simple form would be wrong, keep the precise form and add a definition.

Show the rewritten text. Add a short list of the main changes only when the user asks or when you removed or changed a term that the user may want to keep.

## Before and after

**Before (typical technical text, 1 sentence, 38 words):**
> Retrieval-augmented generation leverages a vector store to facilitate semantic search over chunked documents, whereby the top-k most relevant embeddings are injected into the LLM's context window to ground its responses and mitigate hallucination.

**After (STE style):**
> A language model can only answer from what it learned in training. It does not know your documents. Retrieval-augmented generation (RAG) is a method that gives the model the correct parts of your documents with each question.
>
> First, a program cuts your documents into small parts. It changes each part into an **embedding**. An embedding is a list of numbers that describes the meaning of the text. The program keeps all embeddings in a database.
>
> When you ask a question, the program changes the question into an embedding too. It finds the parts with the most similar embeddings. It sends these parts and your question to the model. The model now answers from your documents and invents less.

## Check before you send

Read your text again and check:

- Is every sentence below the length limit?
- Does each sentence have one idea?
- Is every technical term defined before its first use?
- Do I use the same word for the same thing everywhere?
- Is there a passive sentence where the actor matters?
- Is there a label ("it uses X") without the mechanism?
- Is everything still technically correct?

Do not show this checklist to the user. Fix the text.

## When not to apply the full rules

- The user is clearly an expert and asks an expert question: keep the sentence rules, but do not define terms the user already uses correctly.
- Code, commands, file names and exact error messages stay unchanged. STE rules apply to the prose around them.
- Quotations stay unchanged.