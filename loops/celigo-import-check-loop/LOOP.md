---
name: configuring-imports
title: Configuring Imports skill
repo: celigo/ai
license: MIT
url: https://gethabit.dev/skills/celigo/configuring-imports
---

# Configuring Imports skill

The configuring imports skill helps Celigo builders set up destination steps: adaptor choice, mappings, upsert and matching logic, lookups, hooks, file and AI imports, and safe testing.

- Install the skill: `npx skills add celigo/ai --skill configuring-imports`
- Source: https://github.com/celigo/ai/tree/HEAD/skills/configuring-imports
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a Celigo import; Records get written twice; You set up upsert matching.
Skip it when: You only read data; You do not use Celigo.

# Make it a habit: Celigo imports pass their checklist.

Every Monday your agent lists your Celigo imports, finds orphans with account lint and runs the skill's pre-submit checklist on each one, including duplicate-write guards. It tests through flow test runs, never a real write, and logs findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** checklist items all pass. Hard checks: adaptorType matches the exact case; HTTP lookups send body, not postBody, without the record. prefix; idLockTemplate never renders from {{lookup.; celigo flows test-run finishes without mapping errors. On fail: notify, max 0 retries.
- **Memory:** import check log at `loops/celigo-import-check-loop/runs.md`. Read first: open findings per import from last week.

## Steps

1. **Read the log.** The agent loads last week's open findings.
2. **List imports.** celigo imports list returns every import in the account.
3. **Find orphans.** celigo account lint flags imports that no flow uses.
4. **Run the checklist.** Check required fields, adaptor blocks, lookups and Mapper version for each import.
5. **Check idempotency.** Writes that could repeat need a keyed write and an idLockTemplate from a field the record carries.
6. **Test without writing.** celigo flows test-run with --export uses each import's saved mockResponse instead of the destination.
7. **Log findings.** New and fixed findings go into the run log.

Stop rule: Stops after 20 imports per run.

## Permissions

- Writes: loops/celigo-import-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/celigo-import-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: checklist items all pass. Memory: loops/celigo-import-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
