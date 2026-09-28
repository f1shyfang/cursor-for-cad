# Product

## One line

Engineers mark up the drawings; the software makes the changes; the engineer approves them.

## The problem

Engineers redline drawings, usually in Bluebeam. Someone then has to make every change in Revit by hand, following the firm's families, drafting conventions and title block. In small offices that lands on senior engineers and takes days per markup set, a few thousand dollars of senior time. In firms with juniors it lands on a junior engineer or drafter.

Evidence so far (details in [02-workflow-interview.md](02-workflow-interview.md)):

- Connor spent all 16 hours of one work week in September 2026 completing markups at an electrical comms and security firm, and did the same work at a previous electrical firm.
- Usually under 50 markups a week, so about 20 minutes each. About 90% say exactly what to do (estimate).
- Both firms were standardising their drawing elements at the time.
- At the previous firm, 6 interns (Connor included) did CAD for electrical designs. Many junior engineers describe the same problem, and one firm requires 2 years of CAD before a junior can progress.
- Both data points are electrical engineering firms, so "widespread across disciplines" is not shown yet.

### Obstacles (Startmate Miro, 29 Sep 2026)

> Every time a senior engineer returns a marked-up drawing set, a junior engineer at a small electrical engineering firm has to redo every markup by hand in Revit, one at a time. They work out what the senior meant, find the spot in the 3D model, then place or change the device and fit it to the right wall or ceiling at the right height. It takes about 20 minutes per markup and whole days per set, and the senior then flicks through every sheet to check nothing was missed.

- **Who to call:** owners and senior engineers at small electrical engineering firms who mark up drawings, and the junior engineers and drafters who complete them.
- **Workflow:** turning a senior's Bluebeam markups into Revit changes before the drawings are issued.
- **Constraint:** every change must follow the firm's own families and standards, and the drawings stay in-house, especially on secure government projects.
- **What they do now:** juniors redraw each markup by hand, and seniors check by eye.
- **Consequence:** juniors spend weeks drafting instead of engineering, and seniors lose time checking.

### Drivers: why firms would switch

> Firms will switch because markups eat whole weeks of junior engineering time. One of us spent all 16 hours of a work week on them, and one firm had six interns doing CAD. So firms pay engineering salaries for work that's nine-tenths mechanical. Every revision turns into days of drafting before drawings can be issued, and seniors lose more time checking each sheet by eye. Juniors' first years (two of them, at one firm) go on redrawing instead of engineering.

It is not just faster drafting. It affects salary costs, how fast drawings go out, senior engineers' time, and how quickly juniors become engineers. Still to confirm with owners: that this is in their top 5 problems, and whether it affects hiring and keeping graduates.

## How it works

1. **Standard markup vocabulary.** The firm's engineers mark up with a standard Bluebeam tool set where each symbol means one thing: place a specific Revit family and type, delete, swap type, change a parameter value, move, update a note, revise the title block. Each markup is then structured data (action, family and type, location, values), not a drawing to interpret.
2. **Setup from the firm's own standards.** The tool reads the firm's Revit template, family library and title block and generates their Bluebeam tool set automatically. Early on, the team does this setup as paid onboarding and learns each firm's quirks.
3. **Batch execution.** The whole markup set runs in one pass inside the firm's Revit. Standard markups map directly to Revit API actions: deterministic, local, no AI, no cloud. Each markup's position converts back to model coordinates through its sheet viewport, and each device is hosted on the matching wall or ceiling face of the linked architectural model at the firm's standard mounting height. These are the two slowest manual steps today.
4. **AI only for the leftovers.** Free-form notes and freehand clouds are interpreted by AI and turned into proposed changes from a fixed action vocabulary, or into suggested standard markups for the engineer to confirm. Firms can switch this off.
5. **Approve and verify.** The engineer reviews each proposed change before it is committed. After changes are applied, the tool checks the sheets to confirm every markup was actually done.

**What stays manual:** judgement markups ("resize to suit load", "coordinate with mech", questions). The tool jumps to them and lists them.

## Three tiers of markup

| Tier | Examples | Automatable today? |
|---|---|---|
| 1. Mechanical | Text and note edits, tag and parameter values (cable sizes, device IDs, circuit numbers), type swaps, deletions, revision clouds, revision schedule and title block updates, placing a known family at a marked spot | Yes, with high reliability. The instruction is explicit and the location is exact |
| 2. Geometric | "Move 200 mm left", dimension changes that drive geometry, "add two more like this", rerouting along a sketched path, copying a detail to other sheets | Yes, as a proposal the engineer approves. Sketches are imprecise, so the tool snaps to the model and shows the result before committing |
| 3. Judgement | "Resize to suit load", "coordinate with mech", "check clearance", questions, anything needing calcs, code checks or another discipline | No. The tool jumps to the spot and lists it; the engineer does it |

The realistic ceiling: tier 1 done automatically, tier 2 proposed for one-click approval, tier 3 turned into a clean checklist. The pitch is "days to hours", not "no human".

## Accuracy and running locally

Local models can cost accuracy, and both speed and accuracy matter. The design keeps AI to the smallest possible role:

1. **Standard markups use no AI:** symbol to Revit API action, deterministic, instant, and more accurate than any model.
2. **AI fills a fixed action vocabulary** (for example `set_parameter: size = 25 mm`) instead of reasoning open-endedly, which small local models handle well. Anything outside the vocabulary is impossible, so errors surface as wrong proposals, not wrong drawings.
3. **Workflows are recorded through Revit journal files and API change events**, not screen video, so recording needs no vision model.
4. **Local by default, cloud optional per project**, sending only markup text and a short element-type list, never the model. Secure projects stay local only.
5. **Engineer approval and post-change verification** mean a weaker model produces more flags, not wrong drawings.

Measure it: a test set of markups on public sample drawings, local model against Claude.

## Why it could win

- **Firms keep control.** It runs inside their Revit, on their files, with their families.
- **Firm standards are the moat.** Generic Revit agents can move an element; they do not know a firm's families, title block or conventions, so their output gets redone.
- **Local and deterministic by default**, which answers the security objection on secure government projects, where cloud AI and offshore drafting may both be off the table.
- **Why now:** firms are standardising their drawing elements anyway, Bluebeam supports firm-wide standard tool sets, and Revit 2027 opened up to AI tooling.

## Decisions already made

- **A tool, not a drafting service.** A "send us your markups, get drawings back" service was considered and rejected on 26 Sep 2026: firms want control of their drawings and do the work in-house with their own families, conventions and title blocks.
- **Revit first, AutoCAD later if at all.** 2D has no model, so every sheet is edited separately, and AutoCAD Markup Assist already covers importing markups there.
- **Standard symbols carry most of the load.** Firms are already standardising, so the standard-symbol path does most of the work and AI handles the rest.

## v1 scope

Revit device markups (add, delete, move, swap type) with automatic finding (sheet to model coordinates) and hosting on the linked model at standard heights, because that is where the time goes. Text and tag edits next. An approve-each-change queue, plus a per-markup check report that replaces the senior engineer's flick-through.

## Long-term vision

Start with markups, then grow into every repetitive Revit and document-control task an engineering firm does. Record a workflow once, save it as a repeatable action that runs through the Revit API on the firm's own machines, and build each firm's own library of automations. Later, a request that arrives by email can trigger the right automation, with the engineer stepping in only when the tool is unsure.

As a horizontal product, "record once, automate" is taken (Claude Cowork "Record a Skill", OpenAI Codex "Record and Replay", Power Automate, UiPath, Orby, and YC-stage Understudy, Cyberdesk and Minicor). Its value here is as the vertical, local expansion of this product.
