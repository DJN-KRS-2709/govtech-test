# Decision

Module 12. A data-backed call.

**Call:** Continue, with one change: show each enquiry's drafted priority in the list.

The use case is the Enquiry triage agent for the fictional Harbourlight desk. `GROUP.md` is still blank (PRD gap G1).

## Evidence

| Evidence | What it shows | File |
|---|---|---|
| Usage log, S-1 and S-2 (synthetic) | A person sent 13 of the 20 drafts, and 7 were stopped for review. The draft-then-person flow is used, and the stop fires. | `11-data-and-deploy/data/sample-usage-log.json`, `12-decision/iteration.md` (What moved) |
| Usage log trend (synthetic) | The share sent by a person fell from 9 of 12 in S-1 to 4 of 8 in S-2. | `12-decision/iteration.md` (What did not) |
| Show and swap notes (synthetic, written by Claude) | "They had to open each enquiry to find its priority, so it took them a while to say which one was urgent." | `12-decision/iteration.md` |

Why continue, not pivot or stop: the main promise landed. The screen drafts, and a person sends. The weak spot is how urgency is shown, and the screen can fix that. Nothing in the evidence says the idea fails.

The evidence is thin. There are only two sessions, the notes are synthetic, and no real partner test has run (`12-decision/iteration.md`, Stall).

## The one change

Each enquiry in the list now shows its drafted priority. High priority is marked in red, and a draft that stopped shows "Priority not set". If a person changes a priority, the list updates. The change is in `app/index.html` (`renderList`). It tests the riskiest assumption in `08-validation/validation-brief.md`: a partner can tell from the screen alone which enquiry is urgent.

## Prototype

Artifact link, from the Deploy note in `11-data-and-deploy/fullstack.md`: https://claude.ai/artifact/CTDNiYQ8ToK87Ft11ir8eD

The page at that link is updated with this change. The URL is the same.

## What would change the call

- **Pivot:** a real partner still cannot tell which enquiry is urgent, even with the priority in the list. Then the kill switch fires, and the triage itself is not trusted.
- **Stop:** across more sessions, the share of drafts a person sends keeps falling below the floor in `06-metrics/metrics-plan.md`. That floor is not set yet.
- **Firm up the call:** real show-and-swap notes, a floor in the metrics plan, and real priority levels (PRD gap G5).
