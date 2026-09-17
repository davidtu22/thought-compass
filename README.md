# Thought Compass

A political compass test in the register of *Disco Elysium* and *Zero Parades*: you read a
situation, choose a sentence, and twenty-five interior voices argue with you about it — with
each other, at length, and regardless of which answer you picked.

**[Play it](./index.html)** · [Project note](https://davidtu22.github.io/projects.html)

The compass result is deliberately the least interesting part. The subject is the commentary.

## What's here

| File | What it is |
| --- | --- |
| `Thought Compass.dc.html` | **The source.** Template + logic class. The voice roster, the question bank, the scoring, and the ending table are all plain data inside it. |
| `index.html` | Single-file build — self-contained, no server, no dependencies. This is what GitHub Pages serves. Generated; don't edit. |
| `support.js` | Runtime the source loads. |
| `Voice Bible.dc.html` | Authoring worksheet: five constraint fields per voice (wants / wrong about / never / diction / fights). |
| `Trait Forge.dc.html` | Worksheet for proposing a new voice, including the triage for whether it should exist at all. |
| `Thought Table.dc.html` | The ending table — one Thought per voice, plus ordered pairs. |
| `Writing Room.dc.html` | Drill surface for writing lines against existing scenes. |

Open any `.dc.html` directly in a browser. Read the source in a text editor.

## How it works

**Authored rules, with generation as the exception.** Every statement carries a short
condition list — *if this voice is loud enough, and you took this option, say this.* A match
costs nothing and never drifts. A language model is asked only when nothing matches, and the
result is cached against that exact combination, so it's asked once ever rather than once per
player. The in-app **¶** panel names which path fired, every single time.

That constraint is the whole design. At full coverage the grid holds 288 entries; times five
answers, times twenty-five voices, that's 36,000 possible lines. Nobody writes 36,000 lines —
so the architecture is what makes the ones that *are* written go further.

**Voices, not a scale.** Twenty-five in four clusters: Ledger (reasons at you), Marrow (in the
body), Choir (needs a room), Static (arrives unbidden). Each is a want plus a blind spot — the
blind spot is what makes it a character rather than a position. Volume is adjustable per voice;
below 30 a voice stops matching entirely.

**Conversation, not annotation.** Answers lock before anything replies, then voices arrive one
at a time at a pace you set. Some address each other directly and render as indented replies.
Some take the floor and play a hypothetical out over five paragraphs.

**Memory.** An answer that contradicts an earlier one on the same axis gets read back to you.
Committee minutes the first; Bad Faith takes over from the second, on the grounds that one
contradiction is a mistake and two is a pattern.

**Endings.** A run resolves to a Thought — a name, a description, and a permanent trait —
keyed to the ordered top two voices, with the dominant voice's share setting how hard it
landed. Unwritten pairs fall back to the single-voice row, so the table improves incrementally
and never fails.

## Credits & scope

Original voices, scenarios, and Thoughts. No ZA/UM skill names, dialogue, or art — the debt is
structural and stated rather than borrowed. Written by hand, with a model, about the question of
writing with a model; the ¶ panel exists so that claim is checkable rather than asserted.

Built in Claude Design. Work in progress — the question bank is 76 of a possible 288, and the
pair table is 16 of 132.
