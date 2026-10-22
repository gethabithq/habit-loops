---
name: ccc
title: ccc (CocoIndex Code) skill
repo: cocoindex-io/cocoindex-code
license: Apache-2.0
url: https://gethabit.dev/skills/cocoindex-io/ccc
---

# ccc (CocoIndex Code) skill

The ccc (CocoIndex Code) skill lets an agent run semantic code search over the current codebase with the CocoIndex Code CLI, and keep the index fresh with init and index commands, with language and path filters. For developers searching large codebases.

- Install the skill: `npx skills add cocoindex-io/cocoindex-code --skill ccc`
- Source: https://github.com/cocoindex-io/cocoindex-code/tree/HEAD/skills/ccc
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You search code by concept; You index a codebase after changes; You ask about cocoindex-code.
Skip it when: You need exact text matches only; The repo is tiny.

# Make it a habit: Keep semantic code search fresh.

After significant code changes and at session start, your agent runs ccc index so the semantic index stays current, initializing with ccc init if needed. Searches then use ccc search with language and path filters. A log keeps refresh times.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** code changes land (event; Claude Code routine; `merge to main or session start`)
- **Verification:** index and search work. Hard checks: ccc index exits without error; a known query via ccc search returns at least one result. On fail: retry, max 1 retries.
- **Memory:** index refresh log at `loops/code-index-refresh-loop/runs.md`. Read first: last refresh time and any init errors.

## Steps

1. **Refresh the index.** Your agent runs ccc index from the project.
2. **Init if needed.** On a not-initialized error it runs ccc init from the project root, then ccc index.
3. **Respect exceptions.** It never runs ccc init in the home settings folder and never runs ccc reset itself.
4. **Smoke search.** It runs ccc search for a known concept, with --lang or --path if useful.
5. **Log.** It records the refresh and the smoke search result.

Stop rule: Stops after one index refresh and one retry per run.

## Permissions

- Writes: loops/code-index-refresh-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/code-index-refresh-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: code changes land. Verification: index and search work. Memory: loops/code-index-refresh-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
