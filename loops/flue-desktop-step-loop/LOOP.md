---
name: flue
title: Flue skill
repo: SFKislev/Flue
license: MIT
url: https://gethabit.dev/skills/sfkislev/flue
---

# Flue skill

The flue skill lets a coding agent drive desktop software such as Blender, Photoshop, Premiere and Unity from the shell through a small bridge that returns JSON, for people who want app control without MCP servers.

- Install the skill: `npx skills add SFKislev/Flue --skill flue`
- Source: https://github.com/SFKislev/Flue/tree/HEAD/flue
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want an agent to edit a Blender scene; You script Photoshop or Premiere from the shell; You need live app state as JSON.
Skip it when: The app has no Flue adapter; You want large unattended batch jobs.

# Make it a habit: Desktop app edits, one step.

When you ask for a change in a desktop app, your agent checks Flue is installed, reads the adapter notes, inspects the live app state and runs one small script. The JSON result must report success, you confirm, and a step log keeps what ran.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you request an edit (manual; Claude Code; `manual request naming the app and the change`)
- **Verification:** JSON success + you confirm. Hard checks: flue version answers before any script; bridge script returns JSON on stdout; JSON result reports success, not failure. On fail: stop, max 1 retries.
- **Memory:** step log at `loops/flue-desktop-step-loop/steps.md`. Read first: app, last script and any quirks met.

## Steps

1. **Check Flue.** Run flue version, and if it is missing stop and tell the human that Flue is not installed.
2. **Read the adapter.** Open adapters/<app>/APP.md and search adapters/<app>/docs/api-index.txt with rg for the symbols you need.
3. **Inspect live state.** Use python3 -m flue.cli context <app> to see what the running app holds now.
4. **Run one script.** Send a small, bounded script through python3 -m flue.cli run <app> --stdin.
5. **Read the JSON.** Check that the result on stdout reports success and matches the change you asked for.
6. **Ask before saving.** Ask the human before any save, close, export, render or destructive operation.
7. **Log the step.** Write the app, the script purpose and the result into the step log.

Stop rule: Stops after one small script per run and at most one retry.

## Permissions

- Writes: loops/flue-desktop-step-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flue-desktop-step-loop/steps.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you request an edit. Verification: JSON success + you confirm. Memory: loops/flue-desktop-step-loop/steps.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
