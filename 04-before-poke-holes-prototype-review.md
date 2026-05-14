# Assumption-Targeted Prototype Review (drop-in AI prompt)

Run this on a prototype before a poke-holes session. It is different from a generic "find problems in this flow" review: it points the review at the specific unconfirmed assumptions the prototype was built on, so the session targets actual risk instead of obvious surface issues.

Paste the section below into your AI assistant. Then paste two things: the prototype (or its description / the flow narrative), and the list of ASSUMED and CONTRADICTED requirements from your requirements doc that this prototype depends on.

This pairs with — does not replace — your artifact loop. The artifact loop asks "is this artifact any good." This asks "where does this artifact break if our guesses were wrong."

---

## PROMPT — copy from here to the end of the file

You are reviewing a prototype built by a senior product designer to vet a workflow for a new system. The prototype was generated from a requirements doc, and parts of that doc were ASSUMED rather than CONFIRMED — they are unverified guesses about how the real system behaves. Your job is to find where the user experience falls apart if those guesses turn out to be wrong.

You will be given two inputs: the prototype (or a description of it), and a list of the ASSUMED and CONTRADICTED requirements it depends on. Center the review on that list. A generic usability critique is not what this is for.

This runs in three phases. Do phase one, then stop and wait.

### PHASE ONE — REVIEW

For each ASSUMED or CONTRADICTED requirement in the list, work out what the prototype currently does because it treats that assumption as true, then find what breaks if the assumption is false or partly false.

Output a numbered list:

```
N. [CATEGORY]: <one-sentence finding>. Depends on assumption: <which ASSUMED requirement>. <where in the prototype this shows up>
```

Categories:

- `[BREAKS-IF-WRONG]` — if this assumption is false, the flow does not just look different, it stops working. The user hits a dead end, a loop, or a state the prototype has no screen for.
- `[SILENT-WRONG]` — if the assumption is false, the prototype still "works" but now does the wrong thing, and nothing signals the error. These are the dangerous ones.
- `[MISSING-BRANCH]` — the assumption being false opens a path the user can take that the prototype has no design for.
- `[STATE-GAP]` — a state that only exists, or only does not exist, because of the assumption; if the assumption flips, there is an undesigned state.
- `[CONTENT-FRAGILITY]` — the prototype's content (amounts, labels, statuses, counts) only holds together if the assumption about data shape or range is right.
- `[RECOVERY-GAP]` — if the assumption is wrong, the user ends up somewhere the prototype gives them no way out of.

Then, separately, do one pass for things that are wrong regardless of the assumptions — undefined states, broken back-button behavior, error and interruption cases the flow does not recover from. Label these `[INDEPENDENT]` so they are visibly not assumption-linked.

Aim for 12 to 25 findings total. For each assumption in the list, you should have at least one finding, or an explicit note that the prototype does not actually lean on it.

After the list, stop and say:

> Review saved. Three options:
> 1. Type "continue" to arbitrate as-is.
> 2. Add your own findings as numbered bullets, then say "continue".
> 3. Type "skip N, M, P" to drop findings you do not want arbitrated.

Wait for the designer to respond.

### PHASE TWO — ARBITRATE

When the designer says continue, switch perspective. You are now the designer judging the review. Be fair but firm.

```
N. <VALID | INVALID | PARTIAL>: <one-line reason>
   <VALID: brief plan — does this get fixed in the prototype now, or does it become a question for the poke-holes session because the fix depends on confirming the assumption first?>
   <PARTIAL: which part is valid, which is not>
   <INVALID: why the reviewer is wrong>
```

Many findings here will not have a fix yet — they have a dependency. If a finding says the flow breaks when an assumption is wrong, the right move is often not to redesign the flow now, it is to put that assumption at the top of the poke-holes agenda. Mark those clearly.

### PHASE THREE — REVISE AND ROUTE

Two outputs:

1. **Prototype fixes** — the VALID and PARTIAL findings that can be addressed in the prototype now (independent issues, undesigned states you can just design). Apply them or list them as a concrete change list.
2. **Poke-holes agenda** — the VALID and PARTIAL findings whose real resolution is confirming an assumption. For each: the assumption to confirm, the question to ask, and what the team should watch for in the prototype while discussing it. Sort by blast radius — the assumptions that cause `[BREAKS-IF-WRONG]` or `[SILENT-WRONG]` findings go first.

End with the **Rejected** list: INVALID findings with the one-line reason each.

### Constraints

- You are finding where the prototype is fragile to wrong assumptions. You are not deciding whether the assumptions are true — only stakeholders can do that. Do not rate an assumption as "probably fine" based on how payment systems usually work; treat every item on the list as genuinely unverified.
- No em dashes. Use commas, periods, semicolons, or parentheses.
- Do not invent stakeholder names. Use only names already provided.

## END OF PROMPT

Paste the prototype and the list of ASSUMED / CONTRADICTED requirements below this line.
