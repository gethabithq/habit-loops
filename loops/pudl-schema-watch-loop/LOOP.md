---
name: pudl
title: PUDL skill
repo: catalyst-cooperative/agent-skills
license: MIT
url: https://gethabit.dev/skills/catalyst-cooperative/pudl
---

# PUDL skill

The pudl skill helps energy data users explore PUDL: find tables, read column meanings and usage warnings, and load Parquet from S3 or locally, covering EIA, FERC and EPA data.

- Install the skill: `npx skills add catalyst-cooperative/agent-skills --skill pudl`
- Source: https://github.com/catalyst-cooperative/agent-skills/tree/HEAD/skills/pudl
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You look for US energy data tables; You need a column meaning or warning; You load PUDL data into a notebook.
Skip it when: You need non-US energy data; You are developing the PUDL codebase itself.

# Make it a habit: Know when your PUDL tables change.

Each week your agent fetches the PUDL nightly descriptor with the cache-aware script, uses the datapackage skill to read the tables you depend on, and reports new columns, removed fields and usage warnings. A log keeps last week's schemas.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly descriptor check (schedule; Claude Code routine or cron; `0 6 * * 1`)
- **Verification:** descriptor read, changes listed. Hard checks: python scripts/fetch_descriptor.py exits without error; every watched table is found in the descriptor; usage warnings are listed for each watched table. On fail: notify, max 1 retries.
- **Memory:** watched schemas log at `loops/pudl-schema-watch-loop/run-log.md`. Read first: last week's fields, foreign keys and warnings per table.

## Steps

1. **Fetch descriptor.** Run python scripts/fetch_descriptor.py to refresh assets/cache/.
2. **Query selectively.** Use the datapackage skill's jq patterns for each watched table.
3. **Compare.** Compare fields, schema.foreignKeys and warnings with last week.
4. **Check tiers.** Flag watched tables that are not out_* tables.
5. **Report.** List changes and warnings and log the new schema.

Stop rule: Stops after 20 watched tables per run; reads metadata only, never full tables.

## Permissions

- Writes: assets/cache/**, loops/pudl-schema-watch-loop/**
- Network: s3.us-west-2.amazonaws.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pudl-schema-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly descriptor check. Verification: descriptor read, changes listed. Memory: loops/pudl-schema-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
