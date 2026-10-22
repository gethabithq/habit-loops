---
name: handoff
title: Handoff skill
repo: mattpocock/skills
license: MIT
url: https://gethabit.dev/skills/mattpocock/handoff
---

# Handoff skill

The handoff skill by mattpocock compacts the current conversation into a handoff document for another agent, with suggested skills, links instead of copies and secrets removed. For developers who switch sessions.

- Install the skill: `npx skills add mattpocock/skills --skill handoff`
- Source: https://github.com/mattpocock/skills/tree/HEAD/skills/productivity/handoff
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your context is getting full; You hand work to another agent; You stop for the day.
Skip it when: The task is already done; Everything lives in issues already.

# Make it a habit: Every session ends with a handoff.

At the end of a work session your agent writes a handoff document to the OS temp directory, with a suggested skills section and links to existing specs and commits instead of copies. A check confirms the file exists and holds no secrets.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** session ends (event; Claude Code routine; `user invokes handoff at the end of a session`)
- **Verification:** file and secrets check. Hard checks: the handoff file exists in the temp directory; the document has a suggested skills section; no API key or password pattern appears in the file. On fail: retry, max 1 retries.
- **Memory:** handoff index at `loops/session-handoff-loop/runs.md`. Read first: the path of the last handoff and what the next session was for.

## Steps

1. **Take the focus.** If you passed a note on the next session, your agent tailors the document to it.
2. **Summarise.** It compacts the conversation so a fresh agent can continue the work.
3. **Link, not copy.** It points to specs, plans, ADRs, issues, commits and diffs by path or URL.
4. **Suggest skills.** It adds a suggested skills section for the next agent.
5. **Redact.** It removes API keys, passwords and personal data.
6. **Save and log.** It saves to $TMPDIR or /tmp, not the workspace, and logs the path.

Stop rule: Stops after one handoff document per run.

## Permissions

- Writes: $TMPDIR/**, loops/session-handoff-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/session-handoff-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: session ends. Verification: file and secrets check. Memory: loops/session-handoff-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
