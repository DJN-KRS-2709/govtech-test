# Prototype v3

Module 8. The build that tests the assumption in the validation brief.

## What this version tests

The riskiest assumption in `validation-brief.md`: a partner can tell from the screen alone which enquiry is urgent.

What changed in `app/index.html`: a new **Partner check · kill switch** box sits above the enquiries. The partner looks around the screen with no help, then picks the enquiry they think is urgent, or "I can't tell". The box then says in plain words whether the kill switch fired:

- **Did not fire:** they picked an enquiry the draft marks High. Today that is ENQ-1042, the Harbour Lane streetlight.
- **Fired:** they picked a different enquiry, or could not tell.

The check reads the priority shown on screen. If a person changes a priority, the check uses the new one. "Reset the check" clears the pick for the next partner. Everything else on the screen is the same as in v1.

To open it, follow "How to run it" in `07-prototype/prototype-v1.md`.

## Result

Not run yet. After the partner test, write which enquiry they picked and whether the kill switch fired.

_____

## What you will not polish

This version changes only the partner check. These stay as in v1:

- The drafts are written into the file in advance. No AI runs yet.
- Categories and priority levels are placeholders (PRD gaps G4 and G5).
- Nothing is saved. Picks and edits are lost when the page closes.
