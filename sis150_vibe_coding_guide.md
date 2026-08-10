# Vibe Coding: Working With an AI Coding Assistant — SIS150 Student Guide

Oscar A. Trevizo, Visiting Professor
College of Engineering and Information Science, DeVry University
SIS150 — Fundamentals of Programming | Session 2026.07

This guide explains **how I approach vibe coding**, using a real example
from this course. It does not walk you through your assignment step by
step — that part is yours to do. What it gives you is the *process*:
a repeatable loop you can apply to your own work with an AI coding
assistant, whatever that assignment turns out to ask for.

---

## What is "vibe coding"?

"Vibe coding" is a term for writing software through natural-language
conversation with an AI assistant — describing what you want in plain
English, letting the AI draft the code, then reviewing, testing, and
refining it together — instead of typing every line yourself from a
blank file.

It is **not**:
- Pasting a prompt, getting code back, and turning it in unread.
- A way to skip understanding how the code works.
- A replacement for the fundamentals (variables, control structures,
  functions, classes) you've already been building all term.

It **is**:
- A real, increasingly common way professional developers work.
- A skill with its own good and bad habits, just like debugging or
  testing are skills on top of "knowing how to code."
- Something you can do well or badly — the difference shows in how
  much you actually understand about what got built.

---

## The vibe coding loop

Every good vibe-coding session follows roughly the same cycle, repeated
many times over, not once:

1. **Describe** what you want, in your own words — a feature, a class,
   a fix. Be specific about what "done" looks like.
2. **Generate** — the AI drafts code based on your description.
3. **Review** — read what came back, line by line, the way you'd review
   anyone's rough draft. Does it make sense? Does it match what you
   actually asked for?
4. **Verify** — run it. Does it produce the right output? Does it
   handle the edge cases you care about?
5. **Iterate** — something is almost always off, incomplete, or not
   quite what you meant once you see it running. Say so, specifically,
   and go back to step 1.

The loop is the whole point. A single prompt-and-done exchange isn't
vibe coding — it's just outsourcing. The value comes from the back-
and-forth: catching mistakes, refining requirements as your own
understanding sharpens, and ending up with something you actually
understand because you steered every round of it.

---

## A real example: Module 5's revision history

Open `sis150_module5_inheritance.ipynb` and look at the docstring in
the very first cell. Under **Revision History**, you'll find a dated
log of how that notebook actually got built — not written once, but
shaped over several sessions of exactly the loop above. A few entries,
verbatim:

> **2026-08-01** Renamed VinylRecord -> VinylPressing; added Vinyl45 (a
> has-a composition example) after recognizing a physical single
> realistically holds two songs, not one

This one is a caught mistake. The first design modeled a vinyl single
as holding one song. That's wrong — a real 45 RPM single has an A-side
*and* a B-side. I only realized this because I was reading through
what got generated and comparing it against what I actually know about
vinyl records. The fix wasn't "regenerate everything" — it was a
targeted correction once the gap was spotted.

> **2026-08-01** Major restructuring: inserted SongRecording between
> Song and VinylPressing, since duration/artist need to vary per
> recording (a live take differs from a studio cut; the same song can
> have a different performing artist)

This one is a requirement that only became obvious once the design was
partway built. The original two-level hierarchy (`Song` → pressing)
couldn't represent "the same song, performed differently" — a live
take and a studio cut aren't the same recording, even though they're
the same song. That's a real modeling insight, and it came from
pushing on the design, not from the first draft.

> **2026-08-04** Applied a personal variable-naming convention
> throughout: song1 -> come_together_song, hey_jude_take ->
> hey_jude_rec (it's a SongRecording, not a ReleasedTake -- the old
> name was actually misleading)

This one is a review catch, not a functional bug — the code ran fine
either way. But `hey_jude_take` was actively misleading (it held a
`SongRecording`, not a `ReleasedTake`), and generic names like `song1`
made the notebook harder to read. Neither problem shows up by running
the code — only by reading it carefully and asking "does this name
actually describe what's in the variable?"

Notice what all three have in common: **none of them happened because
the AI got the syntax wrong.** They happened because I was reading the
output critically, checking it against real-world facts I know (how
vinyl singles work), against my own design goals (representing live
takes vs. studio cuts separately), and against plain readability. That
review step is where the actual thinking happens — the AI can draft
fast, but it can't tell you whether the design matches reality unless
you tell it.

---

## What good vibe coding looks like

- You can explain **every line** you turn in, not just the parts you
  wrote by hand.
- You test what you get back — not "it looks right," but actually
  running it and checking the output.
- When something surprises you, you ask **why**, out loud or in the
  chat, before moving on. If the answer doesn't make sense, that's a
  sign to dig further, not to accept it anyway.
- You're willing to throw out a design mid-session once you understand
  the problem better — like Module 5's restructuring above. The first
  draft is a starting point, not a commitment.
- You keep a record of what changed and why, even informally — it's
  how you (and anyone reading your work later) can tell a deliberate
  decision from an accident.

## What to avoid

- Submitting code you can't walk through, line by line, if asked.
- Accepting the first draft without running it.
- Treating a surprising or wrong result as "probably fine" instead of
  investigating it.
- Letting the AI make design decisions you haven't actually thought
  about yourself — the logic, structure, and intent stay yours to own.

---

## Applying this to your assignment

The specifics of what you're building are yours to figure out — that's
the assignment. But the process is the same loop described above:
describe what you want in your own words, review what comes back
critically, verify it actually runs and does what you intended, and
iterate — expecting to revise your own design at least once along the
way, the same way Module 5 went through three real restructurings
before it was done. Copying a result you can't explain carries the
same risk as turning in work that isn't yours — the goal here isn't
a working file, it's a working file *you understand*.
