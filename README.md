# The Assumption Loop

A discovery workflow for turning messy upstream input (stakeholder meetings, system walkthroughs, scattered documentation) into a requirements doc that is safe to hand off and safe to prototype from.

This folder is a private toolkit. Audience: me, and the program managers I work with on a project.

---

## The problem this solves

In discovery, you sit through stakeholder meetings and slowly build a mental model of how a system works. By the time you write the requirements doc, that model feels obvious to you. It is not obvious to anyone who was not in the room, and it is not complete. Every rule you wrote down has an exception you have stopped noticing. That requirements doc then goes two places at once, to PMs for validation and to AI for prototyping, so any gap in it gets inherited by both paths and does not surface until a prototype is already built.

The assumption loop is a set of checkpoints that harden the doc before it propagates.

## How it pairs with the artifact loop

These are two validation loops for two different moments:

- **Artifact loop** validates a thing that has been built (a screen, a prototype, a spec). Adversarial review, arbitration, revision.
- **Assumption loop** (this folder) validates the inputs *before* anything is built.

Same shape — draft, review, arbitrate, revise — applied earlier in the process.

## The one idea everything depends on

Every requirement in the doc carries a status tag:

- **CONFIRMED** — a named stakeholder confirmed it, with a date.
- **ASSUMED** — I am inferring it. The doc records what it is inferred from.
- **CONTRADICTED** — two sources implied different things. Both are recorded, unresolved.

This is the spine. It is what gives the AI prompts something specific to attack, and it is what gives PMs a precise job.

---

## For program managers — start here

You do not need to read all five files. Here is your part:

1. The requirements doc you receive has every requirement tagged CONFIRMED, ASSUMED, or CONTRADICTED.
2. Your review is not "read the whole doc and react." It is: **work the ASSUMED and CONTRADICTED list.** Each of those is a specific question, confirm it, correct it, or kill it.
3. CONFIRMED items already have a source attached. You can spot-check them, but the ASSUMED list is where your time pays off.

That is the whole ask. The doc is structured so your review is fast and high-signal instead of a vague pass over everything.

## For me — how to run it

The five files are drop-in AI prompts. Paste a prompt into any AI assistant, then paste in the material it asks for. Run them in number order across a project:

- `00-START-HERE-workflow-overview.md` — the full map and run-order diagram. Read this first.
- `01-after-each-meeting-gap-audit.md` — run after every stakeholder meeting; produces the next meeting's agenda.
- `02-when-notes-pile-up-contradiction-sweep.md` — run once several sources' notes have accumulated; finds quiet disagreements.
- `03-before-handoff-requirements-review.md` — run on the requirements doc before it goes to PMs or AI; hostile review of the doc itself.
- `04-before-poke-holes-prototype-review.md` — run on a prototype before a poke-holes session; targets the unconfirmed assumptions.

Files 02, 03, and 04 pause partway through for me to edit the findings, then continue to arbitration. That pause is the point — it keeps the loop from being a mirror.

---

## Important limit

These prompts find gaps, contradictions, and undefined states in *how a system is documented*. That is structural work and it is reliable.

They cannot tell anyone what a payment rule, an approval chain, settlement timing, or a compliance requirement *should actually be*, and an AI will confidently invent an answer if asked. Every prompt is instructed to flag those and route them back to stakeholders rather than guess. Internal completeness and consistency are the AI's job. Correctness stays with stakeholders and PMs.

---

## File list

```
README.md                                       this file
00-START-HERE-workflow-overview.md               the map; read first
01-after-each-meeting-gap-audit.md                run after each meeting
02-when-notes-pile-up-contradiction-sweep.md      run when notes accumulate
03-before-handoff-requirements-review.md          run before PM/AI handoff
04-before-poke-holes-prototype-review.md          run before a poke-holes session
```
