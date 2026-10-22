---
name: database-schema-designer
title: Database Schema Designer skill
repo: softaworks/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/softaworks/database-schema-designer
---

# Database Schema Designer skill

Database schema designer designs SQL and NoSQL schemas with normalization, indexing, constraints, relationship patterns and reversible migrations built in. For developers who need production-ready, maintainable data models.

- Install the skill: `npx skills add softaworks/agent-toolkit --skill database-schema-designer`
- Source: https://github.com/softaworks/agent-toolkit/tree/HEAD/dist/plugins/database-schema-designer/skills/database-schema-designer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You design a new schema; You add a table or migration; You review a schema for issues.
Skip it when: You need query tuning only; You have no database.

# Make it a habit: Schema changes pass the design checklist.

On every pull request that touches the schema or migrations, your agent reviews the change against the skill's verification checklist: primary keys, foreign key constraints, indexes on foreign keys, correct data types and reversible migrations. A log keeps open issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** schema or migration change (event; GitHub Actions or Claude Code routine; `pull_request paths: migrations/**, schema/**`)
- **Verification:** design checklist. Hard checks: every table has a primary key; every foreign key has a constraint and an index; money columns use DECIMAL, not FLOAT; every migration has a reversible DOWN step. On fail: notify, max 0 retries.
- **Memory:** schema review log at `loops/schema-review-loop/log.md`. Read first: open schema issues and denormalization decisions made before.

## Steps

1. **Analyze.** Identify the entities, relationships and whether the workload is read-heavy or write-heavy.
2. **Check normalization.** Check the change normalizes to 3NF, or justifies any denormalization for read-heavy access.
3. **Check keys.** Confirm every table has a primary key and every foreign key has a constraint with an ON DELETE strategy.
4. **Check types and indexes.** Confirm DECIMAL for money, date types for dates and indexes on foreign keys and queried columns.
5. **Check migrations.** Confirm each migration has an UP and a DOWN step and adds NOT NULL columns safely.
6. **Log issues.** Record each checklist miss with its table.

Stop rule: Stops after the changed tables and migrations of one pull request.

## Permissions

- Writes: loops/schema-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/schema-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: schema or migration change. Verification: design checklist. Memory: loops/schema-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
