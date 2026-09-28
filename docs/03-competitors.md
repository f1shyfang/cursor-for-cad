# Competitors

First checked 26 Sep 2026. The top 3 were re-checked on their own sites and docs on 28 Sep 2026.

**Summary:** nobody found ships batch execution of a full set of PDF markups made by other people, with verification. Every neighbouring piece exists, and the gap is likely to close within one or two years.

## The gorilla: the status quo

Our primary competitor is the firm's existing markup routine: a senior redlines the PDF in Bluebeam, then a junior opens Revit and makes every change by hand, markup by markup, while the senior checks by flicking through the new PDFs. Put simply: junior engineers redrawing markups themselves.

**What customers do today, when they feel the pain**

- A senior engineer redlines the drawing set in Bluebeam, using symbols, clouds and notes.
- A junior engineer or intern works through it one markup at a time in Revit.
- Each markup takes about 20 minutes: work out what the senior meant, find the spot in the model, place or change the part, and fit it to the right wall or ceiling.
- The senior flicks through the new PDFs against their markups to check nothing was missed.
- One firm makes juniors do 2 years of CAD like this before they can progress.

**Why it is hard to beat**

- It's already paid for: juniors are on salary anyway.
- Firms see it as training, because juniors learn the standards by drafting.
- It's trusted: a person made every change.
- No new software, no setup, no risk.

**How we beat it**

- Same routine, minus the redrawing: seniors still mark up in Bluebeam, and juniors approve changes instead of making them.
- Days of drafting become hours of checking.
- Juniors still learn the standards, by checking every change instead of drawing it.
- Nothing leaves the office, and an engineer approves every change, so the firm keeps control.

**Other alternatives:** offshore drafting (about US$55 a sheet, but the firm loses control of its drawings, and secure government projects may not allow it); hiring another drafter (about A$75k a year, and still manual); the senior engineer doing it themselves in offices without juniors. Competing tools are below.

## Top 3 competing tools

### 1. MarkupX Pro: the direct competitor

Made by MarkupX Inc., resold in Australia and New Zealand by Cadpro.

- **Does:** loads a PDF (markups from Bluebeam, Adobe or Foxit) into Revit, AutoCAD or Civil 3D, lists every markup, zooms to each one in the model, and tracks status. Places a Revit family from a Bluebeam tool chest snapshot with one click. Claims 3+ minutes saved per markup and 5+ minutes per family placement.
- **Falls short:** for hosted families it inserts the family, then the user picks the spot on the host by hand (MarkupX support docs). Setup is manual per family: copy each family and type name into a Bluebeam snapshot's Subject, Layer or a custom column. One markup at a time. No deletes, moves, type swaps, parameter or note changes, no AI for free-form markups, and no check that the change was made.
- **Why it matters:** it is already sold locally and it attacks the two slowest steps (finding and placing). If a firm has seen it and does not use it, the reason is our edge.

### 2. JustAsk for Revit: the AI threat

- **Does:** an AI agent inside Revit with 246 tools. Its Markup panel lets you draw clouds and text on the view, click Ask AI, and the agent reads the sketch and makes the change. Free workspace; Pro US$29/month (founding seats US$15/month). Revit 2025 and 2026.
- **Falls short:** the markup has to be drawn inside Revit by the user, so it does not read a Bluebeam set someone else made. No firm standards. Prompts and a minimal view and selection context go through its proxy to a cloud AI provider (model geometry stays local), which is a problem on secure government projects.
- **Why it matters:** it proves the single-markup mechanic is cheap to build, and it is one feature (PDF import) away from our core.

### 3. Bluebeam Max: the platform risk

- **Does:** it is where the markups are made. Connected Studio Sessions link each markup to its spot in the Revit model. Max connects Revu to Claude through MCP, and Smart Review surfaces issues as markups. Launched May 2026, about US$590 per user per year.
- **Falls short:** it never changes the Revit model.
- **Why it matters:** if Bluebeam, or Autodesk with the Revit 2027 assistant and built-in MCP server, closes the loop, it ships inside software firms already pay for.

## Everyone else

| Player | What it does | Gap |
|---|---|---|
| Autodesk Assistant | Tech preview in Revit 2027 with a built-in MCP server; standalone cross-product agent previewed at AU 2026 | Not a reliable agent yet. Platform risk. Autodesk also says Forma will replace Revit "over time" |
| AutoCAD Markup Import / Markup Assist (since 2023) | Detects text, leaders and clouds in PDF and scanned markups; can start the matching command | AutoCAD only; a human still does the edit |
| SWAPP "Frank" (US$18.5M raised) | Agent that reads and writes the live Revit or ArchiCAD model; proposes, user approves | Architecture-focused, not built around the markup loop |
| ArchiLabs (YC) | Chat-driven Revit automation | General agent, same overlap |
| Endra (US$50M Series A, a16z, Sep 2026) | AI electrical design platform; outputs Revit models; sells to large consultancies | Same discipline, different job (design generation for big firms) |
| Pdftorvt.com (private beta, found 28 Sep 2026) | AI turns PDF plans into a Revit model inside the firm's own template and families; their BIM team calibrates each firm first; claims documents stay on the user's computer; pay only if results are approved | Builds models from plans, does not close markups. Same moat claim as ours (firm standards, paid calibration, local) |
| Revit.Sentinel (RK Tools, public GitHub, found 28 Sep 2026) | Places access-control door sets (reader, contact, lock, REX) around doors in a linked model by rules, in batch, with a per-door review status | Does not read markups. Milestone 1; its README says it has not been exercised in a live Revit session yet; no licence file, so the code is not free to reuse. Shows the hosting step is automatable in our exact discipline |
| Layer (Drawing View) | Annotations link to both PDFs and Revit models | Links markups, does not change the model |
| Offshore drafting services | Redline updates at about US$55 per sheet | The real price anchor, but firms that want control of their drawings keep the work in-house |

Also noted: a Revit YouTuber (Sergio Barata) published "Can AI Build a Revit Model from PDF Markups?" in early 2026, so the do-it-yourself route with Claude is being explored (video titles seen only, not watched).

## Pitch line against MarkupX

> The closest tool out there finds each markup and drops the part in, then leaves you to fit it onto the wall or ceiling by hand, one at a time. We do the whole set, fitting included.

## Sources

- [MarkupX support: Import Revit Elements](https://support.markupx.com/import%20revit%20elements.html)
- [Cadpro: Accelerating your markup experience with MarkupX Pro](https://cadpro.io/knowledge-hub/accelerating-your-markup-experience-with-markupx-pro/)
- [MarkupX](https://markupx.com/), [Cadpro: MarkupX product page](https://cadpro.io/nz/products/markupx/), [AEC Magazine: MarkupX](https://aecmag.com/cad/pdf-markups-delivered-directly-inside-revit-autocad/)
- [JustAsk for Revit](https://justask.xnmakers.com/)
- [Bluebeam: PDF markup in construction guide (2026)](https://www.bluebeam.com/resources/pdf-markup-in-construction-guide-2026/), [Bluebeam Max MCP](https://support.bluebeam.com/revu/resources/revu-mcp.html), [Architosh: Bluebeam Max launch](https://architosh.com/2026/05/ai-powered-bluebeam-max-launches-globally/)
- [Autodesk: Revit 2027 public MCP server](https://help.autodesk.com/cloudhelp/2027/ENU/Revit-WhatsNew/files/GUID-97697CBF-0E11-484E-96E5-4277E3E8D61F.htm), [BIMsmith: Revit 2027 MCP in practice](https://blog.bimsmith.com/Revit-2027-What-the-Built-In-MCP-Server-Actually-Does-in-Practice), [Engineering.com: AU 2026 Autodesk Assistant](https://www.engineering.com/au-2026-autodesks-ai-assistant-is-evolving/)
- [Autodesk: Markup Import and Markup Assist](https://help.autodesk.com/cloudhelp/2026/ENU/AutoCAD-Platform/files/GUID-0CD6B2CE-EAF0-478B-B39B-F4821F9DC91D.htm)
- [SWAPP Frank](https://swapp.ai/products/frank/), [ArchiLabs (YC)](https://ycombinator.com/companies/archilabs)
- [AEC Magazine: Endra launches Power Studio](https://aecmag.com/mep/endra-launches-electrical-design-platform-and-buys-planlabs)
- [Pdftorvt.com](https://www.pdftorvt.com/en)
- [Revit.Sentinel on GitHub](https://github.com/RaulKalev/Revit.Sentinel)
- [Architect Magazine: Layer's Drawing View](https://www.architectmagazine.com/technology/layer-apps-new-drawing-view-connects-pdf-markups-to-revit_o)
- [Sergio Barata: Can AI Build a Revit Model from PDF Markups?](https://www.youtube.com/watch?v=UoW5m8IdkS8)
