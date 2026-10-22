---
name: cli-anything-obsidian
title: CLI Anything Obsidian skill
repo: hkuds/cli-anything
license: Apache-2.0
url: https://gethabit.dev/skills/hkuds/cli-anything-obsidian
---

# CLI Anything Obsidian skill

CLI Anything Obsidian manages an Obsidian vault from the command line through the Local REST API: list, read, create, update, append, search and run commands, with JSON output for agents. For power users automating their notes.

- Install the skill: `npx skills add hkuds/cli-anything --skill cli-anything-obsidian`
- Source: https://github.com/hkuds/cli-anything/tree/HEAD/skills/cli-anything-obsidian
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: managing Obsidian notes from the command line; searching a vault programmatically; letting an agent read and write notes.
Skip it when: the Local REST API plugin is not enabled; you prefer working in the Obsidian GUI.

# Make it a habit: Notes managed without opening Obsidian.

On demand, your agent manages an Obsidian vault through the Local REST API: it checks the server, lists, reads, creates, updates or searches notes, all with JSON output. A run log keeps which notes were touched.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** You ask for note task (manual; Claude Code routine; `run cli-anything-obsidian on demand`)
- **Verification:** server up and note written. Hard checks: cli-anything-obsidian server status reports the API is running; vault list returns files, count above zero; a created or updated note reads back with the expected content. On fail: notify, max 1 retries.
- **Memory:** touched notes log at `loops/obsidian-vault-cli-loop/run-log.md`. Read first: the notes created or changed in earlier runs.

## Steps

1. **Check server.** Your agent runs server status to confirm the Obsidian Local REST API is running before anything else.
2. **List or search.** It runs vault list, search simple or search query to find the right notes.
3. **Read.** It reads a note with vault read in --json mode.
4. **Write.** It creates, updates or appends with the vault commands as the task needs.
5. **Confirm.** It reads the note back to confirm the change and records it in the run log.

Stop rule: Stops after one note task per run, with at most one retry.

## Permissions

- Writes: loops/obsidian-vault-cli-loop/**, the Obsidian vault via the Local REST API
- Network: localhost
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/obsidian-vault-cli-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: You ask for note task. Verification: server up and note written. Memory: loops/obsidian-vault-cli-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
