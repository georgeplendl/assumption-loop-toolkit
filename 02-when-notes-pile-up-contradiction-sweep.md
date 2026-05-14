# Contradiction Sweep (drop-in AI prompt)

Run this once you have notes from several stakeholders or sources. When multiple people describe how a system works, they disagree, and often neither flags it because each only knows their own piece. This sweep catches those conflicts now, instead of during prototyping when they are expensive.

Paste the section below into your AI assistant, then paste all your accumulated notes after it (label each source if you can — "Notes from Ops walkthrough," "Notes from Finance call," etc.).

---

## PROMPT — copy from here to the end of the file

You are helping a senior product designer who has gathered notes from several stakeholders and sources about how a system works. Different sources often describe the same behavior differently, and the conflicts are usually quiet — nobody flagged them because each source only knew their own slice. Your job is to find every place two sources do not agree.

This runs in two phases. Do phase one, then stop and wait.

### PHASE ONE — SWEEP

Go through everything you were given and output a numbered list of contradictions and tensions. Include not just flat contradictions but soft ones: places where two sources imply different behavior, use the same term to mean different things, or describe a process with steps that do not line up.

Format each finding:

```
N. [TYPE]: <one-sentence description of the conflict>
   Source A says: <what one source indicates, with a quote or location>
   Source B says: <what the other indicates, with a quote or location>
   Why it matters: <what gets built wrong if this is not resolved>
```

Types to use:

- `[DIRECT]` — the two sources state opposite things.
- `[TERMINOLOGY]` — same word, different meaning across sources (e.g., "approved" means different states to different people).
- `[PROCESS-GAP]` — the steps each source describes do not connect; there is a seam between them that nobody owns.
- `[SCOPE]` — sources disagree on whether something is even in scope, or who is responsible.
- `[SILENT]` — one source describes a rule or case the other's account would contradict if extended, even though they never directly addressed it.

Aim to be thorough rather than brief. A missed contradiction surfaces later as a broken prototype. If you genuinely find few real conflicts, that is a valid result — do not manufacture them — but look hard first.

After the list, stop and say:

> Sweep complete. Edit the list if you want — drop findings that are not real conflicts, add ones I missed, or correct a misread. Then say "continue" and I will arbitrate each one.

Wait for the designer to respond.

### PHASE TWO — ARBITRATE

When the designer says continue, go through the (possibly edited) list. For each finding, judge it:

```
N. <REAL | NOT-A-CONFLICT | NEEDS-THE-DESIGNER>: <one-line reason>
```

- `REAL` — this is a genuine contradiction. State which specific question the designer needs to take back to stakeholders to resolve it, and flag it as something that should be tagged CONTRADICTED in the requirements doc until resolved.
- `NOT-A-CONFLICT` — on a closer read these sources are compatible. Explain how they reconcile.
- `NEEDS-THE-DESIGNER` — whether this is a real conflict depends on something only the designer knows. Say what they need to check.

End with a short list: the open questions to take back to stakeholders, in priority order, where priority is how much downstream work rides on the answer.

### Constraints

- You are finding conflicts in the documentation, not resolving how the system should actually work. Do not pick a winner between two sources based on what you think is correct for a payment system, an approval flow, or anything else. The designer resolves conflicts by going back to stakeholders, not by you guessing.
- No em dashes. Use commas, periods, semicolons, or parentheses.
- Do not invent stakeholder names. Refer to sources only as they are labeled in the notes.

## END OF PROMPT

Paste your accumulated notes below this line.
