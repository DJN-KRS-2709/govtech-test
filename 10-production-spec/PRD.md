# Production spec

Module 10. Turning a prototype into a production spec. The spec lives in this repo.

This spec describes the screen in `app/index.html` (prototype v3): the Enquiry triage agent for the fictional Harbourlight desk. Every fact names the repo path it comes from. Synthetic data only.

## Problem

| Fact | Repo path |
|---|---|
| A fictional city desk receives many written enquiries, by web form and email. | `03-ai-prd/prd.md` (Problem and user) |
| The assistant drafts a category, a priority, and a short reply. A person reads the draft and decides what is sent. | `use-cases/enquiry-triage-agent.md` (The job) |
| The problem in one sentence is not written yet (PRD gap G3). | `02-idea/problem.md`, `03-ai-prd/prd.md` (G3) |

## In scope: what the screen does

| # | Fact | Repo path |
|---|---|---|
| D1 | Lists four synthetic enquiries, ENQ-1042 to ENQ-1045. Each shows its ID, channel, text, and a status: Draft ready, NEEDS A PERSON, or Checked by a person. | `app/index.html` (`enquiries`, `renderList`) |
| D2 | Shows the selected enquiry with its channel and received time in UTC. | `app/index.html` (`renderDetail`) |
| D3 | Shows the assistant's draft under a "Not sent" label: one category, one priority, and a reply. | `app/index.html` (`renderDetail`) |
| D4 | Lets a person change the category (Streets, Libraries, Permits) and the priority (High, Medium, Low), and edit the reply. | `app/index.html` (`categories`, `priorities`) |
| D5 | Copies the reply to the clipboard. The Copy button is off when the reply is empty. | `app/index.html` (Copy reply) |
| D6 | Lets a person mark a draft as checked, and undo it. | `app/index.html` (Mark as checked by a person) |
| D7 | Stops with NEEDS A PERSON and drafts no reply for ENQ-1044, because the form is not named, and for ENQ-1045, because it asks for a decision about a person. | `app/index.html` (`needsPerson`), `use-cases/enquiry-triage-agent.md` (Checkpoint) |
| D8 | Runs a partner check. The partner picks the enquiry they think is urgent, or "I can't tell". The screen then shows "Kill switch FIRED" or "Kill switch did not fire", with the reason. | `app/index.html` (`renderVerdict`), `08-validation/prototype-v3.md` |
| D9 | The partner check reads the priority on screen. If a person changes a priority, the check uses the new one. A reset clears the pick. | `08-validation/prototype-v3.md` |

## What the screen assumes

| # | Assumption | Repo path |
|---|---|---|
| A1 | The use case is the Enquiry triage agent. `GROUP.md` is still blank (PRD gap G1). | `GROUP.md`, `03-ai-prd/prd.md` (G1) |
| A2 | A partner can tell from the screen alone which enquiry is urgent. This is the riskiest assumption. It is not tested yet. | `08-validation/prototype-v3.md` (What this version tests, Result) |
| A3 | "Urgent" means the draft marks it High. High is a placeholder level (PRD gap G5). | `08-validation/validation-brief.md` (What you will count as a fail) |
| A4 | Streets, Libraries, and Permits are example categories, not the group's list (PRD gap G4). | `app/index.html` (`categories`), `03-ai-prd/prd.md` (G4) |
| A5 | The assistant sees only the text of one enquiry. | `03-ai-prd/prd.md` (What the system may see) |
| A6 | A person sends the reply from the desk's own system. | `app/index.html` (note under the buttons) |
| A7 | The drafts are written in advance. No AI runs on the screen yet. | `08-validation/prototype-v3.md` (What you will not polish) |

## Out of scope: what the screen must not do

| # | Must not | Repo path |
|---|---|---|
| N1 | Send, close, or update a case. The screen has no Send button. | `app/index.html` (banner, note), `03-ai-prd/prd.md` (What it may do) |
| N2 | Draft a reply when it stops with NEEDS A PERSON. | `app/index.html` (`needsPerson`) |
| N3 | Use real enquiry text, ticket numbers from a live system, or resident contact details. | `use-cases/enquiry-triage-agent.md` (Not allowed), `app/index.html` (banner) |
| N4 | Read anything from a live case system. | `03-ai-prd/prd.md` (What the system may see) |
| N5 | Use a database or make network calls. | `app/index.html` (comment at the top) |
| N6 | Claim a live web address. The address is confirmed in class. | `11-data-and-deploy/fullstack.md` |

## Requirements

Each requirement comes from the facts above.

| # | Requirement | Acceptance | From |
|---|---|---|---|
| 1 | Show the draft beside the enquiry, marked as not sent. | Every draft shows the "Not sent" label. | D3 |
| 2 | Never send, close, or update a case. | No control on the screen sends, closes, or updates. | N1 |
| 3 | Stop and hand over when the draft is unsure, or the enquiry asks for a decision about a person. | ENQ-1044 and ENQ-1045 show NEEDS A PERSON and no drafted reply. | D7, N2 |
| 4 | Pick the category and priority only from the lists. | No value outside the lists can be chosen. | D4 |
| 5 | Show whether the kill switch fired. | Picking ENQ-1042 shows "did not fire". Any other pick, or "I can't tell", shows "FIRED". | D8, A3 |
| 6 | Keep memory as files in the repo, not a database. | Enquiries and drafts come from files in `11-data-and-deploy/data/`. No database is added. | Data and memory |

## Data and memory

Memory is files in the repo, not a database. This spec reads one file: `11-data-and-deploy/data/sample-enquiries.json`.

| Fact | Repo path |
|---|---|
| ENQ-1042 to ENQ-1044 live in the data file. Each has empty `category`, `priority`, and `draft_reply` fields. | `11-data-and-deploy/data/sample-enquiries.json` |
| Today the screen reads no file. Its four enquiries and their drafts are written into the page. | `app/index.html` (`enquiries`) |
| ENQ-1045 is only in the page. ENQ-1046 is only in the prompt chain. Neither is in the data file yet. | `app/index.html`, `09-chaining/PROMPTS.md` |
| The data stays in `11-data-and-deploy/data/` until the live address is confirmed in class. | `11-data-and-deploy/fullstack.md` |

## Open gaps

| Gap | Repo path |
|---|---|
| G1 use case, G4 category list, and G5 priority levels shape this screen. G2, G3, G6, and G7 are open too. | `03-ai-prd/prd.md` |
| The partner test has not been run, so the riskiest assumption has no result. | `08-validation/prototype-v3.md` (Result) |
| There is no prototype v2. The file is still the blank template. | `07-prototype/prototype-v2.md` |
