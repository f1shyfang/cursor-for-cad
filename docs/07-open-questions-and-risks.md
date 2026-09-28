# Open questions and risks

## Go and kill signals

- **Go:** tiers 1 and 2 are most of a markup set, and outsourcing is blocked by security or turnaround. The first half is met on Connor's estimate (about 90% spelled out). The second half is open.
- **Kill:** tier 3 (judgement) dominates, or firms happily outsource. Then this is MarkupX with a chatbot.

## The biggest gap (29 Sep 2026)

Every junior engineer asked has the problem, so the work is clearly widespread. What nobody has confirmed yet is the buyer side: owners and senior engineers saying they want it gone and would pay. They may see years of junior CAD as training. Ask them before building past the demo (the 1 Nov gate in [08-plan.md](08-plan.md)).

## Open questions

1. **Has the firm seen MarkupX?** If yes and not used, why not? Ask a senior engineer.
2. **Why don't firms outsource markups?** Security on government sites, turnaround, project context, or habit? Ask a senior engineer.
3. **Would a senior engineer accept tool-made edits** if they approve each one? What is a markup set worth to them? Ask a senior engineer.
4. **Do the seniors' Bluebeam symbols carry a Subject that names the device?** Decides lookup versus shape recognition.
5. **Would engineers use standard symbols for everything** if the tool then did the work? Partly answered: seniors already use tool chest symbols for common devices, and clouds and notes for the rest.
6. **Is it widespread beyond electrical firms?** Both data points so far are electrical engineering firms. The cheapest next data point is someone who has done markups at a civil or structural firm.

## Risks

1. **MarkupX adds AI and more change types.** Speed and firm-standards depth are the defence.
2. **Setup becomes consulting.** Onboarding a firm has to be mostly automatic from its template and family library.
3. **Pricing too low.** Per-seat plugin pricing (JustAsk is US$29/month) is too low; price per firm against hours saved.
4. **Platform risk.** Autodesk (Revit 2027 assistant, a standalone agent in 2027) or Bluebeam could close the loop. Autodesk has also said Forma will replace Revit "over time".
5. **Adoption.** Engineers must use the standard symbols. Firms already standardising is the answer, and the "why now".
6. **Owners see junior CAD as training.** Ask owners early. Juniors still learn the standards by checking every change instead of drawing it.
7. **Licences and IP.** Build on Autodesk Developer Network development licences, not education licences, and check founders' employment contracts for IP clauses.

## Hard rules

1. **Never use real client or employer drawings** as demo data or put them into any AI tool. Connor's day job is on secure government projects, and those drawings are the firm's IP. Demos use public sample models and markups we draw ourselves.
2. **Describe real workflows in words, not screenshots**, when bringing real-world knowledge into this repo.
3. **This repo is public.** No client names, project names, site details or personal contact details.
