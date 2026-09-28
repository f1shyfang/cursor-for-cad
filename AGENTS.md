# AGENTS.md

Context for AI coding agents (Cursor, Claude Code, Codex) working in this repo.

## What we are building

A Revit add-in that reads a set of engineer markups (Bluebeam PDF annotations) and makes the changes they ask for in the firm's own Revit model, using the firm's own families and standards. The engineer reviews and approves every change before it is committed, and the tool then checks that every markup was actually done.

Read [docs/01-product.md](docs/01-product.md) first. Everything else is in [docs/](docs/).

## Current milestone

A demo for Startmate on a public Autodesk sample building: one Bluebeam-marked PDF with about 10 comms and security markups. See [docs/05-demo-and-tech.md](docs/05-demo-and-tech.md) and the build order in [docs/08-plan.md](docs/08-plan.md). Nothing is built yet. The first step is a one-week spike: one symbol on a PDF becomes one device, hosted on the right ceiling of a linked architectural model. The plan proposes a C# Revit add-in; confirm with the team before scaffolding.

## Hard rules

1. **Never use real client or employer drawings** as demo data, test fixtures or AI input. The real-world experience behind this project comes from secure government projects. Build and test only on public sample models and markups we draw ourselves.
2. **Standard markups use no AI.** A standard symbol maps to a Revit action by lookup, and a markup's position maps to model coordinates by geometry. AI is only for free-form clouds and notes, and it must be possible to switch it off.
3. **Local by default.** Nothing leaves the user's machine unless a firm opts in per project, and even then only markup text and a short element-type list, never the model.
4. **Every model change is a proposal first.** Changes are shown for approval, then applied as named, undoable Revit transactions. Nothing is written silently.
5. **Judgement markups are listed, not attempted**, for example "resize to suit load" or "coordinate with mech".
6. **Verify after applying.** Every markup ends as done, flagged with a reason, or listed for the engineer.
7. **This repo is public.** No client names, project names, site details or personal contact details.
