# Discovery-to-Handoff Workflow (for a Senior Product Designer)

This is a process for taking upstream ambiguity (stakeholder meetings, walkthroughs, scattered documentation) and turning it into a requirements doc you can trust enough to hand to PMs and to AI for prototyping. It is built around one idea: the requirements doc is your single point of failure, so the workflow exists to harden it before it propagates.

It pairs with the artifact loop you already use. The artifact loop validates a built thing. This workflow validates the inputs that go into building.

---

## The spine: assumption tags

Everything here depends on one discipline. In your requirements doc, every requirement carries a status tag:

- **CONFIRMED** — a named stakeholder confirmed this, with a date. Write down who and when.
- **ASSUMED** — you are inferring this. Write down what you are inferring it from (a doc, a half-answer in a meeting, analogy to another system).
- **CONTRADICTED** — two sources implied different behavior. Write down both, unresolved.

This is not an AI step. It is a structural change to how you write the doc. It pays off everywhere downstream:

- The AI loops can attack the ASSUMED items specifically instead of treating everything as equally solid.
- PMs get a precise job. They are not "reviewing the doc," they are confirming or killing a specific list of ASSUMED items. Faster for them, higher-signal for you.
- When you prototype, you know exactly which edge cases sit on shaky ground.

If you do nothing else from this workflow, do this.

---

## The four prompts and when to run them

The errors get cheaper to fix the further left you catch them, so the prompts are ordered to catch them as early as possible.

| When | Prompt | What it catches |
|---|---|---|
| After each stakeholder meeting or walkthrough | `01-after-each-meeting-gap-audit.md` | Questions you still cannot answer; what to put on the next agenda |
| Once you have notes from several sources | `02-when-notes-pile-up-contradiction-sweep.md` | Places two stakeholders implied different behavior |
| Before the requirements doc goes to PMs or AI | `03-before-handoff-requirements-review.md` | Rules stated without exceptions, undefined states, unsourced numbers |
| Before a poke-holes session on a prototype | `04-before-poke-holes-prototype-review.md` | Where the UX breaks if a specific unconfirmed assumption is wrong |

### Run order in practice

```
Meeting 1 ──> [01 gap audit] ──> agenda for Meeting 2
Meeting 2 ──> [01 gap audit] ──> agenda for Meeting 3
   ...
(enough notes) ──> [02 contradiction sweep] ──> list of conflicts to resolve
   ...
Draft requirements doc (with assumption tags)
   ──> [03 hostile review] ──> arbitrate ──> revise doc
   ──> doc goes to PMs (they work the ASSUMED list)
   ──> doc goes to AI to prototype
Prototype exists
   ──> [04 prototype review] ──> arbitrate ──> poke-holes session
   ──> (optional) artifact loop on the prototype itself
```

You will loop the early steps many times (one gap audit per meeting) and the later steps once or twice per cycle.

---

## How these prompts work (shared structure)

Prompts 02, 03, and 04 use the same arbitrate-then-revise shape as your artifact loop, because that is what gives them a pass/fail property instead of just generating more text:

1. The prompt produces a numbered list of findings.
2. It stops. You edit, add, or drop findings.
3. You say "continue" and it arbitrates each finding VALID / INVALID / PARTIAL.
4. It applies only what survived.

Prompt 01 (gap audit) is lighter — it just produces a prioritized question list, because there is nothing to arbitrate yet. You have not made claims, you are finding out what to ask.

The arbitration log is the audit trail. All the outputs together show what was challenged, what was kept, what was rejected, and why. That is what you show a skeptical PM or stakeholder.

---

## Important limit (payment-portal specific)

These prompts are good at finding gaps, contradictions, and undefined states in your *documentation* of how a system works. That is structural work and AI is reliable at it.

They cannot tell you what a payment rule, settlement timing, approval-chain logic, or compliance requirement *should actually be*, and an AI will confidently invent one if asked. Keep the prompts pointed at "is this doc internally complete and consistent." Keep "is this doc correct" with your stakeholders and PMs. Every prompt below has this boundary written into it, but it is worth holding in your own head too.

---

## Where this lives

You do not need a new tool. The requirements doc lives wherever your requirements already live. The four prompt files live as files you paste into whatever AI assistant you use. The "workflow" is just knowing which file to paste when, which is what the table above is for.

If you want, keep this overview file pinned next to the requirements doc so the run order is always one click away.
