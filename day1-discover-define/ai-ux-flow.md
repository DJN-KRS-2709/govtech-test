# AI user flow: An officer opens a ServiceSG enquiry and sees a drafted first reply.

**Scenario:** A · ServiceSG enquiry response

All data in this file is synthetic.

## The moment

An officer opens a ServiceSG enquiry and sees a drafted first reply.

## The iceberg

### Above the line: what the user sees

The draft reply, the policy passage it cites next to each line, and Approve, Edit and Restore original buttons.

### Below the line

- Data: Synthetic enquiries (made up) and the public policy pages.
- Model: A language model that drafts the reply and cites the passage it used.
- Rules: No fees, dates or deadlines unless the cited page states them. Never send without an officer.
- Handoffs: Enquiries below the confidence threshold go to an officer with no draft.

## The flow

1. **Trigger:** A resident sends an enquiry to the shared inbox.
   - Trust gap: none
2. **AI step:** Drafts a first reply and cites the policy page for each line.
   - Trust gap: Hallucination. The draft states a fee the policy page does not mention.
3. **Human check:** The officer reads the draft next to the cited passage, edits it, then approves.
   - Trust gap: Black box. The officer cannot see which passage a sentence came from.
4. **Outcome:** The resident gets the reply. The officer’s edits are logged.
   - Trust gap: Control. The officer cannot undo an AI change to their own wording.

## Fallback when the AI is unsure (Advanced)

Below the confidence threshold, no draft. The enquiry goes to an officer with the three closest policy pages.

## How we measure trust (Expert)

Accept-as-is rate: the share of drafts officers send without edits, checked weekly. Target: 6 in 10 by the end of the pilot (made up).
