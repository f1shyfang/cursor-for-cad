# Workflow interview (28 Sep 2026)

Connor's answers about completing markups at work, at an electrical comms and security engineering firm that works on secure government buildings. Estimates, not counts. No drawings or project details are recorded here, on purpose.

## Answers

| Question | Answer |
|---|---|
| Software | Revit mainly, some AutoCAD |
| Markup form | A mix: legend symbols from a Bluebeam tool chest for common devices, clouds and notes for everything else |
| Volume | Usually under 50 markups a week, so about 20 minutes each; sometimes a run of quick ones |
| Where the time goes | Working out what the senior meant and finding the spot in the model; picking the family and hosting it on the linked architectural model at the right height |
| Not the time sink | Device IDs, tags and parameters; knock-ons such as risers and schedules |
| Judgement markups | About 10% |
| How it is checked | The senior flicks through the new PDFs against their markups |

Earlier data point: in one week of September 2026, all 16 hours of Connor's work week went on completing markups. The same work existed at Connor's previous firm, also electrical.

## What it means

1. **The slow part is translation, not thinking.** Finding is geometry: the PDFs are printed from Revit sheets, so each markup's position converts back to a point in the model without AI. Hosting is geometry too: find the wall or ceiling face of the linked architectural model at that point and place the family at the firm's standard mounting height. Decoding a symbol is a lookup table. Only clouds and notes need AI.
2. **Half the go signal is met** (on the estimate): about 90% of markups are spelled out. The other half, whether a firm can outsource secure government work, is still open.
3. **Verification replaces the flick-through.** The tool hands the senior a list of every markup with what was done or why it was flagged, so nothing is missed.
4. **Demo scope:** device markups (add, delete, move, swap type) with automatic finding and hosting. Risers and schedules stay out; they are not where the time goes.

## Still to check

- Do the seniors' tool chest symbols carry a Bluebeam Subject that names the device? If yes, decoding symbols is a lookup (the same kind of field MarkupX reads). If generic, the tool has to recognise the symbol's shape.
- A counted tally of one real set by tier would make the 90% firmer (counts and descriptions only, no drawings).
