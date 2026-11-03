# Prompt chain

Module 9. Chaining prompts so results stay stable. Your group's use case.

Run twice on 3 Nov 2026 on the synthetic enquiry ENQ-1046. Both runs are in the Output slots. Claude ran each step in the Claude app's Code tab, one step at a time, using only that step's prompt with the placeholders filled in. Both runs happened in the same session, so they are a weaker stability test than two fresh sessions. No pass bar failed, so no prompt was edited.

## Chain name

Harbourlight enquiry triage: stop check, then category and priority, then a draft reply.

Built from the PRD, the control panel, the rubric, and `08-validation/validation-brief.md`. `01-context/skill-file.md` is still blank, so the role and rules come from those files. `GROUP.md` is still blank too. This follows the Enquiry triage agent, like every earlier file (PRD gap G1).

Placeholders in the prompts:

- `{{ENQUIRY}}` is the text of one fictional enquiry.
- `{{CATEGORY_LIST}}` is Streets, Libraries, Permits until PRD gap G4 is answered.
- `{{PRIORITY_LEVELS}}` is High, Medium, Low until PRD gap G5 is answered.

## Step 1 · Stop check

### Input

ENQ-1046. Synthetic, written for this run in the same shape as `11-data-and-deploy/data/sample-enquiries.json`. Fictional. Email, received 5 Mar 2026, 08:20 UTC.

> A large branch has fallen across the footpath on Pier Road, outside Harbourlight Library. People are stepping into the road to get past it.

### Prompt

```
You help the fictional Harbourlight desk sort written enquiries.
You draft. You never send, close, or update a case.

Read the enquiry below. Use only its text.
Decide one thing: should a person take over before anything is drafted?
Say NEEDS A PERSON if the enquiry asks for a decision about a person,
or if you cannot tell what it is about. Otherwise say GO.

Reply in exactly this shape:
Decision: GO or NEEDS A PERSON
Reason: one sentence, using only facts from the enquiry.

Enquiry:
{{ENQUIRY}}
```

### Pass bar

- The decision is exactly GO or NEEDS A PERSON.
- The reason uses only facts in the enquiry. No invented name, date, or case number.
- For ENQ-1046 the expected decision is GO. It reports a fallen branch on a footpath and asks for no decision about a person.
- If the decision is NEEDS A PERSON, the chain stops here. Steps 2 and 3 do not run.

### Output

**Run 1**

```
Decision: GO
Reason: The enquiry reports a large branch fallen across the footpath on Pier Road, outside Harbourlight Library.
```

Pass bar: met. GO, as expected. The reason uses only facts from the enquiry.

**Run 2**

```
Decision: GO
Reason: A large branch has fallen across the footpath on Pier Road, and people are stepping into the road to get past it.
```

Pass bar: met. GO, as expected. The reason uses only facts from the enquiry.

## Step 2 · Category and priority

### Input

The same enquiry, plus the Step 1 output. Runs only if Step 1 said GO.

### Prompt

```
You help the fictional Harbourlight desk sort written enquiries.
You draft. You never send, close, or update a case.

Step 1 said GO for the enquiry below.
Pick one category from this list only: {{CATEGORY_LIST}}
Pick one priority from this list only: {{PRIORITY_LEVELS}}
If no category fits, or you are unsure, write NEEDS A PERSON instead.

Reply in exactly this shape:
Category: one item from the list
Priority: one item from the list
Why: one sentence, using only facts from the enquiry.

Enquiry:
{{ENQUIRY}}
```

### Pass bar

- The category is on the list. An invented category fails (rubric: Category).
- A second person would pick the same priority. Aim for 4 or higher out of 5 (rubric: Priority).
- The priority does not ignore an urgent safety line in the enquiry.
- The reason uses only facts in the enquiry.

### Output

**Run 1**

```
Category: Streets
Priority: High
Why: A large branch blocks the footpath on Pier Road, and people are stepping into the road to get past it.
```

Pass bar: met. Streets is on the list. The mention of Harbourlight Library did not pull it into Libraries. High does not ignore the safety line about people stepping into the road.

**Run 2**

```
Category: Streets
Priority: High
Why: The branch is across the footpath on Pier Road, and people are stepping into the road to get past it.
```

Pass bar: met. Same category and priority as Run 1.

## Step 3 · Draft reply

### Input

The same enquiry, plus the Step 2 output: the category and the priority.

### Prompt

```
You help the fictional Harbourlight desk sort written enquiries.
You draft. You never send, close, or update a case.
A person reads your draft and decides what is sent.

Write a short reply to the enquiry below.
Use only facts that are in the enquiry.
Do not add a name, a date, a case number, or a promise.
Where the reply needs something only the desk knows, such as what
happens next, write [Person to add: ...].
Do not say the reply has been sent.

Category: {{CATEGORY}}
Priority: {{PRIORITY}}
Enquiry:
{{ENQUIRY}}
```

### Pass bar

- Faithful: every fact is in the enquiry. Any "no" fails outright (rubric).
- No extras: no invented resident name or case number. Any "no" fails outright (rubric).
- A person could send it after a light edit. Aim for 4 or higher out of 5 (rubric: Reply).
- It reads as a draft. It does not say it has been sent.

### Output

**Run 1** (Category: Streets, Priority: High)

```
Thank you for telling us about the large branch that has fallen across the footpath on Pier Road, outside Harbourlight Library. We understand people are stepping into the road to get past it.

[Person to add: what happens next.]
```

Pass bar: met. Every fact is in the enquiry. No name, date, case number, or promise. It does not say it has been sent.

**Run 2** (Category: Streets, Priority: High)

```
Thank you for letting us know that a branch has fallen across the footpath on Pier Road, outside Harbourlight Library, and that people are stepping into the road to get past it.

[Person to add: what the desk will do about the branch.]
```

Pass bar: met. Same facts as Run 1. No name, date, case number, or promise.

The Reply score (4 or higher out of 5) is a judgement for a person. Score both drafts with `05-evals/human-rubric.md`.

## What must stay the same on a second run

Run the same enquiry through the chain again. These must not change:

- Step 1: the decision.
- Step 2: the category and the priority.
- Step 3: the facts in the reply, and every pass bar still met. The wording may change.

Result for ENQ-1046: all held. Both runs gave GO, then Streets and High, then a reply with the same facts. Only the wording changed.
