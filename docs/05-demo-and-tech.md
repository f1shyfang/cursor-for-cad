# Demo and technical approach

## The Startmate demo (first milestone)

- **Model:** a public Autodesk sample building as the architect's linked model, with our own comms and security model linking it. Built with a student Revit licence.
- **Markups:** one Bluebeam-marked PDF with about 10 comms and security markups: mostly tool chest symbols (cameras, card readers, duress buttons and similar), a few clouds and notes, and one judgement call.
- **Run:** the tool reads the markups, finds each spot, hosts each device on the right wall or ceiling at standard height, handles deletes, moves and type swaps, and queues every change for approval.
- **End:** a check report listing every markup as done, flagged with a reason, or left for the engineer, then a before and after of the sheets.
- **Proof point:** time by hand against time with the tool.

Nothing is built yet. A full build plan (tooling, schedule) is still to be written.

## Technical approach (from the 26 Sep 2026 research)

- **Digital markups are the easy case.** Bluebeam markups are structured PDF annotations: type, exact coordinates, text, author, colour, Subject and custom columns. Nothing needs to be "seen". Scanned pen markups are much harder: on the AECV-Bench benchmark, models read text in drawings well (up to 0.95 accuracy) but symbol understanding and counting remain weak.
- **Finding *where* is deterministic, not AI.** A PDF printed from Revit maps from sheet coordinates to viewport to view to model coordinates through the Revit API. Bluebeam's Connected Studio Sessions already does this kind of linking. AI is only needed for *what* a free-form markup means and *which element* it refers to.
- **Decoding a standard symbol is a lookup.** MarkupX reads the Revit family and type from a snapshot's Subject, Layer or a custom column. We can do the same, and generate the firm's tool set from its family library so nobody copies names by hand.
- **Hosting on linked models needs face-based or work-plane-based families.** Wall-hosted families cannot be hosted by linked walls. Placement means finding the wall or ceiling face of the linked architectural model at the markup's point, then placing the family at the firm's standard mounting height. Revit.Sentinel's README documents the same constraint for door hardware.
- **Doing the change is solved plumbing.** Revit add-ins run changes as normal, undoable transactions. Revit 2027 ships a built-in MCP server (tech preview), and third-party Revit MCP servers expose 138 to 216 tools, including parameter edits, type swaps, tagging and element creation.
- **The differentiator is verification.** After applying changes, re-export the sheet and check each markup was actually done. Nobody found does this, and it is what makes a senior engineer trust the output.
- **Skip AutoCAD for v1.** 2D has no model, so every sheet is edited separately, and AutoCAD Markup Assist already covers importing markups there.

## Sources

- [AECV-Bench](https://arxiv.org/pdf/2601.04819)
- [Autodesk: Revit 2027 public MCP server](https://help.autodesk.com/cloudhelp/2027/ENU/Revit-WhatsNew/files/GUID-97697CBF-0E11-484E-96E5-4277E3E8D61F.htm)
- [BIMsmith: Revit 2027 MCP in practice](https://blog.bimsmith.com/Revit-2027-What-the-Built-In-MCP-Server-Actually-Does-in-Practice)
- [MarkupX support: Import Revit Elements](https://support.markupx.com/import%20revit%20elements.html)
- [Revit.Sentinel on GitHub](https://github.com/RaulKalev/Revit.Sentinel)
