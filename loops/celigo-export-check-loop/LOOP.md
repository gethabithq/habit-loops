---
name: configuring-exports
title: Configuring Exports skill
repo: celigo/ai
license: MIT
url: https://gethabit.dev/skills/celigo/configuring-exports
---

# Configuring Exports skill

The configuring exports skill helps Celigo builders set up source and lookup steps: adaptor choice, delta and once syncs, webhooks, file transfers, CDC listeners, pagination and GraphQL.

- Install the skill: `npx skills add celigo/ai --skill configuring-exports`
- Source: https://github.com/celigo/ai/tree/HEAD/skills/configuring-exports
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a Celigo export; An export returns no records; You set up a delta sync.
Skip it when: You only write data; You do not use Celigo.

# Make it a habit: Celigo exports keep returning records.

Every Monday your agent lists your Celigo exports, finds orphans with account lint and runs the skill's pre-submit checklist: delta setup, resource paths, mock output shape and file deletion. Record exports get a live invoke, and findings go into a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** checklist passes, records return. Hard checks: delta exports set type delta and delta.startDate; celigo exports invoke returns at least one record for record-based exports; mockOutput uses the page_of_records shape; no export carries a rest: block. On fail: notify, max 0 retries.
- **Memory:** export check log at `loops/celigo-export-check-loop/runs.md`. Read first: open findings and record counts per export from last week.

## Steps

1. **Read the log.** The agent loads last week's findings and record counts.
2. **List exports.** celigo exports list returns every export in the account.
3. **Find orphans.** celigo account lint flags exports that no flow uses.
4. **Check delta setup.** Delta exports need type delta, delta.startDate and lastExportDateTime as the lower bound.
5. **Check file exports.** Files another reader needs must set file.skipDelete to true.
6. **Invoke record exports.** celigo exports invoke reads the live source without saving, and zero records points at resourcePath.
7. **Log findings.** Findings and record counts go into the run log.

Stop rule: Stops after 20 exports per run.

## Permissions

- Writes: loops/celigo-export-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/celigo-export-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: checklist passes, records return. Memory: loops/celigo-export-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
