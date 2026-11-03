# Access rules

Module 11. Written and tested with Claude Code against the synthetic files in `data/`.

These rules are for the Enquiry triage agent at the fictional Harbourlight desk. `GROUP.md` is still blank, so this follows the use case in every earlier file (PRD gap G1). The role switch in `app/index.html` follows this table. This role switch is a prototype. It is not real authentication and not a database.

## Roles

| Role | Can read | Can write | Must not |
|---|---|---|---|
| Desk staff | Every enquiry: text, channel, and received time. The assistant's draft: category, priority, and reply. | The draft's category, priority, and reply. Mark a draft as checked. | Send, close, or update a case from this screen. Edit the enquiry text. |
| Reviewer | Every enquiry and its draft. Usage counts for enquiry triage. | A score from 1 to 5 for each draft, kept on this page only. | Edit the enquiry or the draft. Send, close, or update a case. |
| Applicant | Their own enquiry only: text, channel, and received time. In this prototype, the fictional sender of ENQ-1042. | Nothing on this screen. There is no sign-up. | See another person's enquiry. See the unsent draft, the scores, or the usage counts. |

## Data the page reads

The page copies two files into itself. It fetches nothing.

| File | What the page uses |
|---|---|
| `data/sample-enquiries.json` | All three rows, ENQ-1042 to ENQ-1044. |
| `data/sample-usage-log.json` | The two enquiry triage sessions, S-1 and S-2. The reviewer sees them. |
| `data/sample-applications.json` | Nothing. It belongs to the Application helper use case. |

The drafts and ENQ-1045 are written into the page for the prototype. They are not in the data files.

## Test you ran

Run by Claude Code on 3 Nov 2026. Headless Chrome opened `app/index.html`, picked each role, and pressed **Check**. The page check reads what is on the screen at that moment.

| Test | What the page showed | Result |
|---|---|---|
| Desk staff, press Check | "Hidden correctly: Send, close, and update controls." No button sends, closes, or updates a case. | Pass |
| Reviewer, press Check | "Hidden correctly: Edit controls for the draft." Category, priority, and reply are read-only. | Pass |
| Applicant, press Check | "Hidden correctly: Other people's enquiries." None of the other 3 enquiries is on the screen. The partner check is hidden too. | Pass |
| An unknown role value | The page showed the Applicant view, the narrowest one. | Failed closed |
| Applicant, with the partner check forced back on | "Not hidden: Other people's enquiries. Visible: ENQ-1043, ENQ-1044, ENQ-1045." | The Check caught the leak |

Two more checks:

- The JSON inside the page is identical to `data/sample-enquiries.json` and `data/sample-usage-log.json`.
- The page has no fetch, no links to other files, and no sign-up.

Limit: the role switch only hides things on the screen. All the data is still in the page source, so anyone who opens the source can read it. This role switch is a prototype. It is not real authentication and not a database.
