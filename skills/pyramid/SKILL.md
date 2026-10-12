---
name: pyramid-explanation
description: Explain any topic as a "pyramid" of four plain-language layers with hard word limits — at most 8, 16, 64 and 128 words (32 is deliberately skipped). Use this skill whenever the user asks for a pyramid explanation, says "pyramid" or "Pyramide" about an explanation, asks to explain something "in 8 / 16 / 64 / 128 words", wants an explanation "in layers", "from short to long", or "zoomable".
disable-model-invocation: true
---

# Pyramid Explanation

Explain the requested topic in four layers. Each layer is a complete, standalone explanation — a reader who stops after any layer should walk away with a correct (if coarser) picture. The layers get longer, not just wordier: each one adds something the previous one could not fit.

## The four layers

| Layer | Word limit |
|---|---|---|
| 1 | ≤ 8 |
| 2 | ≤ 16 |
| 3 | ≤ 64 |
| 4 | ≤ 128 |

32 is skipped on purpose. Do not add a 32-word layer.

The limits are hard maxima. Aim for roughly 75–100 % of each limit — a 3-word layer 1 or a 40-word layer 3 wastes the room the reader was promised. Never go over.

## Plain language is the point

The less jargon, the better. Write for a curious, intelligent person outside the field.

- Prefer everyday words and short sentences.
- Concrete images beat abstract definitions ("like a library index card" beats "a metadata pointer structure").
- Don't trade correctness for simplicity. A simple but wrong statement is worse than a slightly longer true one. If something must be simplified, simplify by leaving detail out, not by saying something false.


## Output format

Answer in the language the user wrote in. Use exactly this structure, with the actual word count of each layer in parentheses:

**8 words** (n)
<layer 1>

**16 words** (n)
<layer 2>

**64 words** (n)
<layer 3>

**128 words** (n)
<layer 4>

No intro sentence, no closing summary, no follow-up offer — the pyramid is the whole answer. Translate the labels if the user writes in another language (German: "8 Wörter").

Especially in layer 4 consider 1-2 line breaks where it makes sense.

## Example

User: pyramid: what is a hash function?

**8 words** (8)
A machine that gives any data a fingerprint.

**16 words** (16)
It turns any data into a short fingerprint, so computers can quickly check or find things.

**64 words** (60)
You feed in anything — a word, a photo, a whole movie — and get back a short, fixed-length string of characters. The same input always gives the same string. Change one letter and the string changes completely. That makes it handy for spotting tampering, checking downloads, and finding items fast, like using a page number instead of reading the whole book.

**128 words** (128)
A hash function takes data of any size and squeezes it into a short code of fixed length, called a hash. Think of it as a fingerprint: tiny compared to the person, but it identifies them. The same data always produces the same hash, and even a tiny change produces a totally different one. Websites store hashes of passwords instead of the passwords themselves, then compare hashes at login. Download pages publish hashes so you can confirm your file arrived undamaged. Databases use hashes to jump straight to stored items. Two limits matter. First, the process only runs one way: you cannot rebuild the data from its hash. Second, because endless inputs share a limited number of codes, two different inputs can occasionally collide on the same hash.

Note how layer 4 defines "hash" itself instead of leaning on earlier layers, and ends with limits rather than a summary.

## Edge cases

- **Topic too vague** ("pyramid: physics"): pick the most likely meaning and explain that; don't ask a clarifying question first unless the topic is truly unguessable.
- **User asks for different word limits**: use theirs, keep the same principles.
- **Contested or opinion topics**: describe what the thing is and the main positions; don't pick a side to save words.