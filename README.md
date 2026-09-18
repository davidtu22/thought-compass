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

## The shift: from instrument to stage

I started this wanting a very customizable political compass test. I ended up wanting something
closer to a chunk of *Disco Elysium* torn out and set down on its own, and the distance between
those two things is most of the work.

**What I was originally building.** A compass with more axes than the standard two, a question
bank you could edit, adjustable voices commenting on each answer. The commentary was a layer on
top of an instrument. The instrument was the point; the voices were the personality.

**Where that broke.** The voices had nothing to push against. A scale answer — agree, strongly
agree — isn't a position, it's a coordinate, and there's nothing in a coordinate for a character
to have an opinion about. So the commentary came out as annotation: one clever line per voice per
answer, technically responsive, structurally inert. I could feel it going stale within three
playthroughs, and more statements wouldn't have fixed it, because the format was the ceiling.

**What I diagnosed.** The thing that makes those games work isn't that the skills are witty. It's
that there's *context* — a story, characters, scenarios — so nothing a voice says feels isolated
or abrupt. Every line is contextual, and the answer options themselves are the writing: in
*Disco Elysium* the choices don't feel like different ways of answering the same question, they
feel like genuinely ideological and sometimes very funny representations of every way a real
person might respond to a situation that's half serious and half absurd. Somebody once described
it as reading like an infinite collection of good tweets. That's the register — and a survey
scale cannot produce it, no matter how good the commentary layered on top is.

**What I changed, in order.** Scales became scenarios with written answer options, each one an
honest position rather than a degree of yes. Reactions stopped appearing the moment you touched
an option — you have to lock in, because the tension lives in the commitment. The lines got
longer, because a voice needs room to be specific. And then the decisive one: voices started
addressing *each other* and bickering, and one per scene got permission to take the floor and
ramble — to play a hypothetical all the way out over five paragraphs instead of landing a quip.

**Where that leaves the compass.** Secondary, deliberately. I care much less about where someone
falls on an axis than about the voices tearing into them for the answer they chose, no matter
which one it was. That's the quippy, playful, slightly unbearable thing that makes those games
engaging — the sense that your own head is an argument you are losing. The axes still work, the
scoring is still honest, and the dot still lands somewhere. It's just no longer what the thing
is for.

**What this repo is actually a portfolio piece for.** Writing. The scenarios, the answer options,
the voices, and the constraint system that makes a roster of twenty-five stay distinct across
hundreds of lines. The architecture exists to serve that, and the worksheets in here are the part
I'd point at first — they're the discipline, not the output.

## Design log

Built across one long session. The sequence matters more than the feature list, because most
of the architecture exists in response to a specific complaint about the previous version.

**Three visual directions, then a commitment.** Paper-of-record (the portfolio's own cream and
oxblood), Nightshift (oil and ash), and Case File (an intake form with margin stamps). Nightshift
won, with one amendment: give each voice its own hue, so the roster reads as an assortment rather
than a palette.

**A coverage grid before any content.** Eight axes by twelve domains, three slots per cell — 288
entries at full coverage. The point of the grid is that any subset you switch on still scores
honestly, because the denominator is computed from what's active. That made it safe to write
slowly.

**The voice bible came from me being wrong.** I drafted twelve voices in a literary register.
Four came back rewritten much blunter and more explicitly ideological — Actuary as Chicago-school
tech-bro, Committee as *"Authoritarian! We condemn!"*, Room Read answering one scene with a bare
em dash and nothing else. The em dash is still the best line in the build. I rewrote the other
eight to match that ear, not mine.

**Memory, then memory that isn't monotonous.** First version had Committee cite question numbers
when you contradicted yourself. The complaint was fair: it named the question like a clerk and
accused you of hypocrisy far too fast for contradictions that were actually nuanced. Rewritten
so nothing cites a number and the voices get progressively more agitated instead — Committee
minutes the first, Bad Faith takes over from the second, on the grounds that one contradiction
is a mistake and two is a pattern.

**Scale answers were the real ceiling.** Agree-to-disagree gave the voices nothing to push
against. Converted to scenarios with written answer options, each one a genuine position rather
than a degree of yes — the true believer, the one who already spent the money, the one who
negotiates a smaller version of the same compromise, the refusal that costs something specific.
That single change is what let the voices start doing anything interesting.

**Tension needed a lock.** Reactions used to appear the instant you touched an option and change
if you changed your mind. Now nothing answers until you commit, and then the voices arrive one
at a time at a pace you set.

**Twenty-five voices, because twelve wasn't a roster.** *Disco Elysium* has 24 traits; *Zero
Parades* has 15 skills. Twelve felt thin by comparison, so thirteen more were proposed and
approved — Casuistry, Falsification, Inventory, Appetite, Flinch, Last Ditch, Bedside, Grievance,
Pulpit, Rapture, The Bit, Vertigo, and Composition for the aesthetic judgement the set was
missing.

**Then the same six kept showing up.** Diagnosed as mechanical rather than authorial: when more
voices matched than the per-answer cap allowed, they were taken in authored order, and the
obvious voice tends to get written first. Now the app prefers whoever has spoken least this run.
Self-balancing, so new writing doesn't reintroduce it.

**Tirades.** The last and largest change. The brief was explicitly that the compass result
matters less than the voices tearing into you, so voices can now address each other and render
as indented replies, and one voice per scene can take the floor and play a hypothetical out over
five paragraphs — the year after you sign the sponsorship, the fourth week of the month you
refused it.

**On writing this with a model.** The note in the app used to read *"nobody writes 480 lines."*
That was corrected, and the correction is worth keeping: there are whole teams of writers in
studios who write out those lines one by one, a feat the tech industry is broadly uninterested
in crediting. The position here isn't that generated writing is forbidden — it's that it should
be the exception you can point at, which is why the ¶ panel names the path every line took, and
why the lines that matter were written by hand.

## Credits & scope

Original voices, scenarios, and Thoughts. No ZA/UM skill names, dialogue, or art — the debt is
structural and stated rather than borrowed. Written by hand, with a model, about the question of
writing with a model; the ¶ panel exists so that claim is checkable rather than asserted.

Built in Claude Design. Work in progress — the question bank is 76 of a possible 288, and the
pair table is 16 of 132.
