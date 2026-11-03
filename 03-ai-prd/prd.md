# AI requirements

Module 3. Writing AI requirements engineers can build from. Your group's use case.

Built from `03-ai-prd/harness-sketch.md`, `use-cases/enquiry-triage-agent.md`, and the synthetic file `11-data-and-deploy/data/sample-enquiries.json`. Anything those files do not say is marked **Gap** and left open.

**Gap G1 · Use case.** `GROUP.md` is still blank. This PRD assumes the Enquiry triage agent, because the harness sketch describes it. Confirm the group's use case.

## Problem and user

A fictional city desk receives many written enquiries, by web form and email. The assistant reads one enquiry and drafts a category, a priority, and a short reply. A person at the desk reads the draft and decides what is sent.

**Gap G2 · User.** Who reads the drafts? Name the role at the fictional desk.

**Gap G3 · Problem.** `02-idea/problem.md` is blank. What goes wrong at the desk today, in one sentence?

## What the system may see

Sources it can read. Name fictional ones. Say what you left out.

- The text of one fictional enquiry, pasted for each run. Samples: ENQ-1042 to ENQ-1044 in `11-data-and-deploy/data/sample-enquiries.json`, plus new ones the group writes in the same shape.
- The category list.

Left out:

- Anything from a live case system.
- Real enquiry text, ticket numbers from a live system, and resident contact details.
- Earlier runs. It has no memory, so every run starts fresh.

**Gap G4 · Category list.** The list is not written yet. The use case names streets, libraries, and permits only as examples. What are the group's categories?

**Gap G5 · Priority levels.** Nothing says what the priority levels are. Which levels can it choose from?

## What it may do

The verb list. Mark each verb read, draft, or send. Sending requires a person.

| Verb | Type | Who |
|---|---|---|
| Read the enquiry text | read | Assistant |
| Read the category list | read | Assistant |
| Draft a category | draft | Assistant |
| Draft a priority | draft | Assistant |
| Draft a reply | draft | Assistant |
| Send the reply | send | A person only |
| Close the case | send | A person only |
| Update the case | send | A person only |

Closing and updating change the case, so they count as send. Drafting is automatic. Nothing leaves the desk until a person checks it.

## When it stops

Turn limit, and the trigger that hands the work back to a person.

- Turn limit: one pass per enquiry. Then the draft goes to a person.
- It stops and hands the draft to a person if the draft is unsure, or if the enquiry asks for a decision about a person.

**Gap G6 · Unsure.** Nothing checks the draft yet. How does the assistant show that it is unsure, so the person knows to look closer?

## What a good answer looks like

Known so far:

- One category, taken from the category list.
- One priority.
- A short reply that a person can read and then decide to send.

**Gap G7 · Good enough.** Nothing checks the output yet, and there is no rubric. What makes a reply good enough to send: length, tone, what it must say? Module 5 builds the rubric.
