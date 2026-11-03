# Iteration notes

Module 12. What you changed after looking at the synthetic usage log and the show-and-swap notes.

Sources:

- **Usage log:** `11-data-and-deploy/data/sample-usage-log.json`. Synthetic, not a live analytics export. Only the two enquiry triage sessions count here: S-1 and S-2. S-3 belongs to the Application helper use case.
- **Show and swap notes:** none were pasted. The request still said "[paste the show and swap notes]", and `08-validation/show-and-swap-notes.md` is still blank. As asked, Claude wrote the synthetic notes below on 3 Nov 2026. No real partner test or show and swap happened. Replace them with your group's real notes.

> **Synthetic show and swap notes (written by Claude, not from a real session)**
>
> What they understood: The other group saw straight away that the screen only drafts and a person sends.
>
> What they stumbled on: They had to open each enquiry to find its priority, so it took them a while to say which one was urgent. They did not know why ENQ-1044 stopped until they read the NEEDS A PERSON box.
>
> What we will change: Show the priority on each enquiry in the list.

## What moved

- People sent drafts in both sessions. In S-1, a person sent 9 of the 12 drafts. In S-2, a person sent 4 of the 8.
- The stop is in use. Drafts were stopped for review in both sessions. In S-2 the log shows `"stopped_for_review": 4`.
- From the notes, the main promise landed: the screen drafts, and a person sends.

## What did not

- The share of drafts sent by a person fell, from 9 of 12 (75%) in S-1 to 4 of 8 (50%) in S-2. The share stopped for review rose, from 3 of 12 (25%) to 4 of 8 (50%).
- Urgency is still hard to see. From the notes: "They had to open each enquiry to find its priority, so it took them a while to say which one was urgent." That is the riskiest assumption in `08-validation/validation-brief.md`.
- The log does not say why a draft was stopped. It only counts stops, so there is no way to tell a good stop from a bad draft.

## Stall

These block a firm continue, pivot, or stop call:

- **Too little data:** two sessions and 20 drafts are not enough to tell a trend from noise.
- **No real partner test yet:** the Result in `08-validation/prototype-v3.md` is still blank, and the notes above are synthetic.
- **No target to compare against:** `06-metrics/metrics-plan.md` on `main` is still the blank template, so there is no floor for "sent by a person".
- **Placeholder levels:** the categories and priority levels are still placeholders (PRD gaps G4 and G5), so priority accuracy cannot be judged yet.
