---
name: openspec-bulk-archive-change
title: OpenSpec Bulk Archive Change skill
repo: fission-ai/openspec
license: MIT
url: https://gethabit.dev/skills/fission-ai/openspec-bulk-archive-change
---

# OpenSpec Bulk Archive Change skill

The openspec bulk archive change skill archives several finished OpenSpec changes at once, resolving spec conflicts by checking the codebase and asking one confirmation, for teams running parallel spec work.

- Install the skill: `npx skills add fission-ai/openspec --skill openspec-bulk-archive-change`
- Source: https://github.com/fission-ai/openspec/tree/HEAD/skills/openspec-bulk-archive-change
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Several changes are finished; Changes touch the same spec; You say openspec archive all.
Skip it when: Only one change is done; Changes are still in progress.

# Make it a habit: Clear finished changes in batches.

At the end of each sprint your agent lists active OpenSpec changes, lets you pick which to archive, checks status and spec conflicts against the codebase, asks one confirmation, then syncs, verifies and archives each change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** end of sprint (schedule; Claude Code routine; `0 16 * * 5`)
- **Verification:** you confirm the batch. Hard checks: openspec list --json returns every selected change; included deltas match main specs after sync; no archive move nested inside an existing folder. On fail: stop, max 0 retries.
- **Memory:** archive folder at `openspec/changes/archive/`. Read first: archived changes and skipped sync notes.

## Steps

1. **List changes.** Run openspec list --json and stop if no active changes exist.
2. **You select.** Ask you to pick changes; never pick them on your own.
3. **Validate batch.** Run openspec status --change with --json for each and check task counts and archive targets.
4. **Find conflicts.** Map delta specs by capability path and flag paths touched by two or more changes.
5. **Resolve conflicts.** Search the codebase for implementation evidence and decide which deltas to sync.
6. **Confirm once.** Show a status table and ask one batch question.
7. **Sync and archive.** Run openspec-sync-specs inline for included deltas, verify, then move each change.
8. **Summarize.** Report archived, skipped and failed changes plus sync results.

Stop rule: Stops after one batch per run.

## Permissions

- Writes: openspec/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`openspec/changes/archive/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: end of sprint. Verification: you confirm the batch. Memory: openspec/changes/archive/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
