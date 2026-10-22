---
name: indexion-identity
title: Indexion Identity skill
repo: trkbt10/indexion-skills
license: Apache-2.0
url: https://gethabit.dev/skills/trkbt10/indexion-identity
---

# Indexion Identity skill

Indexion identity detects name and content drift in functions, files and folders with indexion identity audit, then plans verified renames, moves or splits. For maintainers who want code names to keep matching what the code does.

- Install the skill: `npx skills add trkbt10/indexion-skills --skill indexion-identity`
- Source: https://github.com/trkbt10/indexion-skills/tree/HEAD/skills/indexion-identity
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You suspect stale file names; You plan a folder cleanup; You want to split overgrown files.
Skip it when: You need a quick variable rename; Your project does not use indexion.

# Make it a habit: Names keep matching what code does.

Each week your agent runs indexion identity audit, treats each row as a candidate, verifies it with doc graph, grep and rg, and makes the smallest confirmed rename, move or split. Tests must pass, and the JSON report keeps the queue for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly name drift audit (schedule; Claude Code routine; `0 7 * * 1`)
- **Verification:** moon test + re-audit. Hard checks: moon test passes; moon fmt leaves no changes; indexion identity audit runs again after the changes. On fail: retry, max 1 retries.
- **Memory:** identity report queue at `.indexion/cache/identity/report.json`. Read first: candidates still open from the last audit.

## Steps

1. **Run the scan.** Run indexion identity audit with --format=json into the report file.
2. **Review candidates.** Compare name, expected summary, actual summary, assessment and recommendation for each row.
3. **Verify first.** Check each candidate with indexion doc graph, indexion grep --semantic and rg.
4. **Make one change.** Pick the smallest confirmed operation: rename a symbol, file or folder, move a file or split it.
5. **Re-check.** Run moon info, moon fmt, moon test and the identity audit again.

Stop rule: Stops after at most 5 confirmed changes per run, with 1 retry.

## Permissions

- Writes: src/**, .indexion/cache/identity/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.indexion/cache/identity/report.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly name drift audit. Verification: moon test + re-audit. Memory: .indexion/cache/identity/report.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
