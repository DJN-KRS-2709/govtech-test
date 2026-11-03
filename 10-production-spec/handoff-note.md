# Handoff note

Module 10. What an engineer needs that the spec does not already say.

This note is for the Harbourlight enquiry triage screen in `app/index.html`. The spec is `10-production-spec/PRD.md`. Synthetic data only. There is no database: memory is files in the repo.

## Data files

Three JSON files sit in `11-data-and-deploy/data/`. All three are synthetic. The screen must not edit them.

| File | What one row holds | Rows | Does the screen read it? |
|---|---|---|---|
| `sample-enquiries.json` | One fictional written enquiry to the Harbourlight desk. For example, ENQ-1042: a streetlight on Harbour Lane that has been dark for three nights. | 3: ENQ-1042 to ENQ-1044 | **Yes.** It is the only file the spec reads (`10-production-spec/PRD.md`, Data and memory). Today the screen holds a copy of these three rows inside `app/index.html` and reads no file. |
| `sample-applications.json` | One fictional room-booking application, with the fields that are still missing. It belongs to the Application helper use case. | 2: APP-220 and APP-221 | No. It is not part of enquiry triage. |
| `sample-usage-log.json` | One synthetic usage session: drafts made, drafts sent by a person, and drafts stopped for review. Its note says it is seeded for Module 12. | 3: S-1 and S-2 for enquiry triage, S-3 for the application helper | No. The screen does not use it. |

### What the screen reads from `sample-enquiries.json`

| Field | In the file today | Where it shows on the screen |
|---|---|---|
| `id` | Filled, such as ENQ-1042 | The enquiry list and the enquiry heading |
| `received` | Filled, a UTC date and time | The enquiry heading, shown in UTC |
| `channel` | Filled: web form or email | The enquiry list and the enquiry heading |
| `text` | Filled, the enquiry in one sentence | The enquiry list and the quoted enquiry |
| `category` | Empty | The draft's Category. The assistant's draft fills it. |
| `priority` | Empty | The draft's Priority. The assistant's draft fills it. |
| `draft_reply` | Empty | The draft's Reply. The assistant's draft fills it. |

## How to run the prototype

From "How to run it" in `07-prototype/prototype-v1.md`:

1. Go to https://github.com/DJN-KRS-2709/govtech-test.
2. Open the `app` folder, then click `index.html`.
3. Click **Download raw file**. It is the download icon at the top right of the file view.
4. Double-click the downloaded `index.html`. It opens in a web browser with no sign-in and no internet connection.

## Known gaps

| Gap | Repo path |
|---|---|
| The screen reads no file yet. Its enquiries and drafts are written into the page. | `app/index.html` (`enquiries`) |
| The data file has no field for a stop. The screen's `needsPerson` and `reason` have no matching field in `sample-enquiries.json`. | `app/index.html`, `11-data-and-deploy/data/sample-enquiries.json` |
| ENQ-1045 is only in the page. ENQ-1046 is only in the prompt chain. Neither is in the data file. | `app/index.html`, `09-chaining/PROMPTS.md` |
| The categories and priority levels are placeholders (PRD gaps G4 and G5). | `03-ai-prd/prd.md` |
| The partner test has not been run. | `08-validation/prototype-v3.md` (Result) |
| There is no live web address yet. It is confirmed in class. | `11-data-and-deploy/fullstack.md` |

## Decisions already made

| Decision | Repo path |
|---|---|
| The assistant drafts. A person sends. Nothing sends, closes, or updates a case. | `10-production-spec/PRD.md` (N1) |
| When the draft is unsure, or the enquiry asks for a decision about a person, the screen shows NEEDS A PERSON and drafts no reply. | `10-production-spec/PRD.md` (D7, N2) |
| Category and priority come only from the lists. | `10-production-spec/PRD.md` (Requirement 4) |
| Memory is files in the repo, not a database. | `10-production-spec/PRD.md` (Data and memory) |
| Synthetic data only. No real enquiry text, live ticket numbers, or resident contact details. | `use-cases/enquiry-triage-agent.md` (Not allowed) |
| The data stays in `11-data-and-deploy/data/` until the live address is confirmed in class. | `11-data-and-deploy/fullstack.md` |
