# Prototype v1

Module 7. Building a working prototype in one session. Claude Code writes code into `app/`.

## What I built

The first screen of the Enquiry triage agent for the fictional Harbourlight desk. It is one file: `app/index.html`.

Purpose: a desk person picks one enquiry and sees the assistant's draft beside it: a category, a priority, and a reply. They can change any part, copy the reply, and mark the draft as checked. The screen never sends. It has no Send button.

- Four synthetic enquiries. ENQ-1042 to ENQ-1044 come from `11-data-and-deploy/data/sample-enquiries.json`. ENQ-1045 was written for this prototype in the same shape.
- The drafts are written into the file in advance. No AI runs yet. There is no database, and nothing is stored, so edits are lost when the page closes.
- Two enquiries stop with NEEDS A PERSON. ENQ-1044 stops because the text does not say which form, so the draft is unsure. ENQ-1045 stops because it asks for a decision about a person.

Open gaps from the PRD that show on this screen:

- **G1 · Use case.** `GROUP.md` is still blank. This screen assumes the Enquiry triage agent.
- **G4 · Category list.** Streets, Libraries, and Permits are the examples from the use case, not the group's list.
- **G5 · Priority levels.** High, Medium, and Low are placeholders.

## Riskiest assumption this version touches

A person at the desk can tell, on one screen, what the assistant drafted and what still needs them. A draft is never mistaken for a sent reply.

This is a proposal based on the worked example. Replace it if your group names a different riskiest assumption in `02-idea/problem.md`.

## How to run it

1. Go to https://github.com/DJN-KRS-2709/govtech-test.
2. Open the `app` folder, then click `index.html`.
3. Click **Download raw file**. It is the download icon at the top right of the file view.
4. Double-click the downloaded `index.html`. It opens in your web browser. It needs no sign-in and no internet connection.
