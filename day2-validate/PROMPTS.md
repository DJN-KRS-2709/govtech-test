# Prompt chain

**Scenario:** A · ServiceSG enquiry response
**Prototype today:** Shows the ServiceSG enquiry inbox with made-up enquiries and a drafted first reply for each one.

All data is synthetic and labelled as made up.

## 1. Expand

**Prompt:** Let the officer filter the inbox by policy topic, and show the topic on each enquiry.

**Business rules:**
- Topics come from a fixed made-up list of 6.
- An enquiry can have one topic only.

**Edge cases:**
- An enquiry that matches no topic goes under Other.
- The filter shows a count of 0 without breaking.

**Result:** _fill in after you run it: what worked, what broke._

## 2. Behavior

**Prompt:** Handle a failed policy lookup: show a clear message, keep the officer’s draft, and offer a retry.

**Forced failure:** Make the policy lookup return nothing for every enquiry about fees.

**Business rules:**
- Never show a draft that cites no policy page.
- Never lose text the officer typed.

**Edge cases:**
- The lookup fails twice in a row.
- The officer edits the draft while the retry runs.

**Result:** _fill in after you run it: what worked, what broke._

## 3. Refine

**Prompt:** Make labels, spacing and button names consistent on the reply screen.

**Business rules:**
- Do not change how drafts are generated or approved.

**Edge cases:**
- Long enquiries still fit on a laptop screen.

**Result:** _fill in after you run it: what worked, what broke._
