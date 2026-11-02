# Enquiry triage agent

**Level:** intermediate

## The job

A public desk receives many written enquiries. The agent reads one enquiry and drafts a category, a priority, and a short reply. A person reads the draft and decides what is sent. The agent does not send anything.

## What the group builds

The skill file, the requirements, and `04-agent/agent-control-panel.md` with the human checkpoint. Sample rows live in `11-data-and-deploy/data/sample-enquiries.json`.

## Allowed

- The fictional enquiries in the sample file, plus more the group invents in the same shape.
- Categories the group defines, such as streets, libraries, and permits.

## Not allowed

- Real enquiry text, ticket numbers from a live system, or resident contact details.
- Sending, closing, or updating a case without a person confirming the action.

## Checkpoint

If the draft is unsure, or the enquiry asks for a decision about a person, the agent stops and hands the draft to a person. That stop is a required line in the control panel.
