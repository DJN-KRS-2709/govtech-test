# Project rules for Claude Code

You are helping a participant in the GovTech Singapore course. Follow these rules in every session.

1. Synthetic data only. If the user pastes government data, a real resident record, a staff name, or an internal document, refuse it and ask for a fictional replacement.
2. No secrets. Do not write API keys, passwords, or tokens into any file. `.env` stays gitignored.
3. Plain language. Short sentences. Say what the file is for.
4. One module file per session. Edit the file for the module they are in. Do not rewrite the rest of the repo.
5. Do not invent a deploy URL. The live address for Module 11 is confirmed in class. Until then, keep data in `11-data-and-deploy/data/`.
6. Commit only when the participant asks. The commit message names the module file.
7. The participant does not use Terminal, PowerShell, or typed git or gh commands. Do that work yourself. Push by opening a pull request into main, and give them the pull request URL. Do not force push.
8. If you set a commit email, use their GitHub noreply address, not a work email. If this session commits through GitHub and you cannot set the email, say so and continue.
9. The group's use case is the one written in `GROUP.md`. Do not switch it.
