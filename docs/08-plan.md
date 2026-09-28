# Plan (29 Sep 2026)

A draft to argue with, not a commitment.

## Where things stand

- **Problem evidence:** Connor's own 16-hour week of markups in September 2026; 6 interns, Connor included, doing electrical CAD at a previous firm; many junior engineers describing the same thing; one firm that makes juniors do 2 years of CAD before they can progress.
- **The gap:** no firm owner or senior engineer, the people who pay, has been asked yet.
- **Product:** nothing built yet. The demo is specified in [05-demo-and-tech.md](05-demo-and-tech.md).

## The product

### Who it is for

| Role | Who | What they need |
|---|---|---|
| Buyer | Owner or principal of a small electrical engineering firm (under 20 staff per office) | Drawings out on time without burning engineer hours |
| User | Whoever completes markups: junior engineers, drafters, sometimes seniors | Markups done in minutes, correctly, to the firm's standards |
| Reviewer | The senior engineer who marked up the drawings | Confidence that every markup was done, without flicking through |

### The loop

1. The senior marks up the PDF in Bluebeam as usual: standard symbols where the firm has them, clouds and notes for the rest.
2. The user opens the add-in in Revit and loads the marked-up PDF.
3. The tool reads every markup, works out the sheet, the spot in the model and the action, and proposes each change.
4. The user steps through the proposals: approve, edit or reject. Judgement markups are listed, not attempted.
5. The tool applies the approved changes as one undoable step, then checks each markup and writes a report.
6. The senior reads the report instead of flicking through the PDFs.

### Markup vocabulary (v1)

| Markup on the PDF | Action in Revit | Tier |
|---|---|---|
| Device symbol from the firm's tool chest | Place that family and type at the spot, hosted on the right ceiling or wall at the standard height | 1 |
| The firm's "Delete" tool, or a cross over a device | Delete the element | 1 |
| A different device symbol over an existing device, or "change to X" | Swap type | 1 |
| Tag or ID change | Set the parameter | 1 |
| The firm's "Move" arrow from a device to a new spot | Move, shown for approval | 2 |
| Cloud with a free-form note | AI proposes one action from this list, or flags it | 2 |
| Question, "coordinate with mech", "resize to suit load" | Listed for the engineer | 3 |

### How it is built

| Part | Job | Notes |
|---|---|---|
| Markup reader | Read every annotation in the PDF: type, Subject, custom columns, position, text | C# with a permissively licensed PDF library. PdfPig is Apache 2.0, with annotation access marked experimental, so confirm it reads Bluebeam's fields in the spike. Keep AGPL libraries (iText, PyMuPDF) out of the product unless licensed |
| Sheet locator | Match each PDF page to its Revit sheet, and each markup's position to a point in the model through the sheet's viewport | Deterministic, no AI. One of the two biggest technical unknowns |
| Interpreter | Turn each markup into one action from the vocabulary | Symbols: a lookup table in the firm's config. Clouds and notes: AI behind a switch |
| Host resolver | Find the ceiling or wall face of the linked architectural model at that point, and the mounting height | The other big unknown. Revit's ReferenceIntersector can hit geometry in linked models. Face-based families can be hosted on linked faces; wall-hosted families cannot |
| Review queue | List proposals, zoom to each, approve, edit or reject | Modeless WPF window, the pattern Revit.Sentinel uses |
| Apply and check | Apply approved changes as one undo step, confirm each markup was done, write the report | Report as HTML or PDF |
| Firm config | Map symbol Subjects to family types, heights and host rules | Generated from the firm's family library; later it also generates their Bluebeam tool chest |

**Stack:** a C# Revit add-in. Target Revit 2026 first, since firms usually run a version or two behind (check what pilot firms run). AI for free-form notes sits behind one interface: the Claude API for the demo, and a local open-weight model (for example Qwen2.5 7B, Apache 2.0) for firms that cannot use the cloud. The Revit 2027 built-in MCP server is fine for exploring but not the core: it is a tech preview and not deterministic.

**Licences:** the student Revit licence is for education only, not for-profit work. Autodesk Developer Network's start-up membership is free for up to 3 years and includes Autodesk software for development. Revit and Bluebeam Revu both have 30-day trials; start the Bluebeam trial the day the build starts. Client firms already own Revit and Bluebeam, so the add-in runs on their licences.

### Build order

1. **Spike (week of 5 Oct): one symbol becomes one device on the right ceiling.** A public sample building linked into an electrical model, a face-based camera family, a sheet printed to PDF, one symbol placed in Bluebeam, and code that reads it, maps it, finds the ceiling and places the device. This retires the two biggest unknowns: coordinate mapping and hosting on linked models.
2. **Demo (by 1 Nov): the 10-markup set.** Six device placements, a delete, a move, a type swap, one cloud with a note read by AI, and one judgement markup flagged. Review queue, one-step undo, check report. Time the same set by hand for the before and after.
3. **Test set (alongside):** marked-up sample PDFs with known right answers, run after every change. It doubles as the accuracy test for AI on free-form notes: local model against Claude.
4. **Pilot product (Dec to Feb):** the full tier-1 vocabulary, firm config generated from a family library, an installer, local logs, report export.
5. **Paid v1 (2027):** Bluebeam tool chest generation, the local AI option, more Revit versions, licensing.

**Not in v1:** AutoCAD, scanned pen markups, risers and schedules (not where the time goes), anything cloud-based by default, design calculations.

### After v1

1. **More disciplines on the same engine:** mechanical, hydraulic and fire services also mark up and draft in Revit.
2. **Revisions and title blocks:** revision clouds, revision schedules, issue sheets.
3. **Record once, repeat:** record a firm's repetitive Revit tasks through journal files and API events, and replay them on demand.
4. **Requests by email** trigger the right automation, with the engineer approving.
5. **Other countries** where firms draft in Revit.

## Go-to-market

- **Beachhead:** small electrical engineering firms that do their own Revit drafting, starting with comms and security on government projects, where keeping drawings in the building matters most.
- **First conversations:** the warm network first (former and current colleagues, the junior engineers already spoken to and their firms), then direct outreach to owners on LinkedIn and at Engineers Australia events.
- **Design partners:** 2 to 3 firms get a free 3-month pilot on their own machines, in exchange for measured before-and-after times and a reference.
- **Later channels:** Autodesk resellers (Cadpro sells MarkupX this way) and the Autodesk App Store.

### Getting started

Talk and build at the same time: owner conversations from this week, the demo from 5 Oct. No client is needed to start building, and no licence needs buying.

**Conversations before the demo exists** follow The Mom Test: ask about the last markup set, who did it, how long it took and what they have tried, without pitching. End each one by asking for something with a date, such as "Can I show you a working demo in October?" Send outreach from personal email or LinkedIn, not university accounts.

Outreach message:

> Hi [name], I'm a final-year electrical engineering student at UQ, working part-time in electrical design. I'm researching how small electrical firms handle drawing markups: the redlines seniors hand back to be updated in Revit. Could I ask you a few questions in a 15-minute call this week? I'm not selling anything yet.

**First client, as a free pilot (design partner):**

1. One-page pilot agreement: free for 3 months, runs on their machines, nothing leaves their office, their engineers approve every change (so the firm stays responsible for its drawings). In return: feedback, measured times, and a reference if it works.
2. Measure the "before": time 2 or 3 real markup sets done by hand.
3. Set it up to their standards on their machine: read their family library and map their Bluebeam symbols.
4. Start on one computer and a non-secure project, sitting next to whoever does their markups.
5. Check in weekly: fix what broke, measure minutes per markup.
6. At the end, if time per markup has halved, ask them to pay the monthly fee.

**Before anyone pays:** agree ownership between the founders, then register a company (Pty Ltd). No money taken as individuals.

## Pricing (to test, not settled)

- A monthly fee per office, starting around A$400 to 1,000, anchored to "less than one week of a junior's salary" (A$75k a year is about A$1,440 a week).
- Paid onboarding to set up the firm's standards.
- Free for design partners.

## Milestones and gates

| When | Milestone | Keep going if |
|---|---|---|
| 29 Sep | Bootcamp pitch | |
| 30 Sep to 4 Oct | Conversations only: 5 owner calls booked, the three questions for a senior engineer, ADN application | |
| 5 to 11 Oct | Spike | A symbol lands as a device on the right ceiling |
| By 1 Nov | Demo working; 10 owner conversations logged | At least 3 owners would pilot or pay |
| November | Demo video. Startmate Accelerator application if an intake is open | |
| Dec to Feb | 2 to 3 design partners on the pilot product | Measured time per markup at least halves |
| 2027 | First paying firms | Firms pay and renew |

## Risks

| Risk | What to do |
|---|---|
| Owners don't care: juniors are cheap and CAD is "training" | Gate at 1 Nov: ask owners before building past the demo |
| MarkupX adds hosting, batching and AI | Move fast on the full vocabulary and firm standards |
| Autodesk or Bluebeam closes the loop | Stay local, standards-deep and firm-specific |
| Setup turns into consulting | Generate the firm config from the family library from day one |
| An employer claims the IP | Check founders' employment contracts for IP clauses; build on your own time and machines, on public sample models only |
| Using education licences for the company | ADN start-up membership before building the demo |

## Open decisions

1. **Beachhead:** comms and security on government projects first, or all small electrical firms.
2. **Startmate:** apply to the Accelerator this intake, or after pilots.
3. **Hours:** what each founder commits per week until the demo is done.

## Sources

- [Autodesk Developer Network membership (start-up offer)](https://aps.autodesk.com/developer/overview/autodesk-developer-network-membership)
- [Autodesk: educational licences and terms](https://knowledge.autodesk.com/customer-service/account-management/education-program/free-education-access/licenses-for-students-educators)
- [PdfPig on GitHub (Apache 2.0)](https://github.com/UglyToad/PdfPig)
- [Revit.Sentinel README](https://github.com/RaulKalev/Revit.Sentinel) for linked-model hosting and the review-window pattern
