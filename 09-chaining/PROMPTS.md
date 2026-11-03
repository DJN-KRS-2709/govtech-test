# Prompt chain

Module 9. Chaining prompts so results stay stable. Your group's use case.

The chain is written but not run yet. Every Output slot is empty on purpose.

## Chain name

Harbourlight enquiry triage: stop check, then category and priority, then a draft reply.

Built from the PRD, the control panel, the rubric, and `08-validation/validation-brief.md`. `01-context/skill-file.md` is still blank, so the role and rules come from those files. `GROUP.md` is still blank too. This follows the Enquiry triage agent, like every earlier file (PRD gap G1).

Placeholders in the prompts:

- `{{ENQUIRY}}` is the text of one fictional enquiry.
- `{{CATEGORY_LIST}}` is Streets, Libraries, Permits until PRD gap G4 is answered.
- `{{PRIORITY_LEVELS}}` is High, Medium, Low until PRD gap G5 is answered.

## Step 1 · Stop check

### Input

ENQ-1042 from `11-data-and-deploy/data/sample-enquiries.json`. Fictional. Web form.

> The streetlight on Harbour Lane has been out for three nights.

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
- For ENQ-1042 the expected decision is GO. It reports a street fault and asks for no decision about a person.
- If the decision is NEEDS A PERSON, the chain stops here. Steps 2 and 3 do not run.

### Output

_____

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

_____

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

_____

## What must stay the same on a second run

Run the same enquiry through the chain again. These must not change:

- Step 1: the decision.
- Step 2: the category and the priority.
- Step 3: the facts in the reply, and every pass bar still met. The wording may change.
