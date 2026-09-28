# Pitch

## Customer problem statement (draft, 28 Sep 2026)

| Prompt | Answer |
|---|---|
| **Our customer is** | Small electrical engineering firms (under 20 staff per office) that do their own Revit drafting, starting with comms and security firms on government projects. |
| **Who is trying to** | turn senior engineers' marked-up drawings into an updated Revit model and sheets, to the firm's own standards, before the drawings are due to be issued. |
| **But struggles because** | every markup is done by hand, one at a time. Each takes about 20 minutes, mostly finding the spot in the model and fitting the part onto the right wall or ceiling. One of us spent all 16 work hours of a week in September 2026 on it, and existing tools still leave most of it by hand. |
| **And will still switch because** | about 9 in 10 markups say exactly what to do, so they're paying engineers for mechanical work while real design waits. And switching is low-risk. It works inside the Revit and Bluebeam they already use, with their own families and standards. Nothing leaves the building, which matters on secure government jobs, and an engineer approves every change. |

The "starting with" clause is optional: it is where the evidence comes from, and where keeping drawings in the building matters most.

## One-minute pitch draft (no slides)

> Last week I spent all 16 hours of my engineering job doing one thing: taking the changes engineers had marked up on drawings and redrawing them in Revit by hand. About nine in ten of those markups said exactly what to do. The hours went on finding each spot in the model and fitting each device onto the right wall or ceiling. I did the same thing at my last job. In small firms it's senior engineers losing days per drawing set. Existing tools help you find each markup, then leave you to do the work. We're building software that does the work: engineers mark up with their firm's standard symbols, and our tool makes every change in their own Revit, to their own standards, and they approve each one.

"Nine in ten" is Connor's estimate from the 28 Sep 2026 interview. A counted tally of one set would make it firmer.

## Lines to keep ready

- **Against MarkupX:** "The closest tool out there finds each markup and drops the part in, then leaves you to fit it onto the wall or ceiling by hand, one at a time. We do the whole set, fitting included."
- **Tighter existing-tools line:** "Existing tools show you where each markup is and place one part per click. Nothing does the whole set and checks it." The draft's "then leave you to do the work" undersells MarkupX's one-click placement, and a mentor who knows MarkupX could call it out.
- **On AI accuracy:** standard markups use no AI at all. AI only proposes changes for free-form notes, and the engineer approves every change.
- **On security:** it runs locally inside the firm's own Revit, and secure projects never touch the cloud.

## Keep the cost stories separate

At a firm with juniors, the markups are junior time; at small offices they are senior time. Do not mix the two numbers.
