---
name: neon-postgres
title: Neon Postgres skill
repo: neondatabase/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/neondatabase/neon-postgres
---

# Neon Postgres skill

The neon postgres skill guides your agent on Lakebase Postgres on Neon: pooled or direct connections, migrations on branches, read-only inspect checks and search. For developers with an existing Neon database.

- Install the skill: `npx skills add neondatabase/agent-skills --skill neon-postgres`
- Source: https://github.com/neondatabase/agent-skills/tree/HEAD/plugins/neon-postgres/skills/neon-postgres
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: you have a Neon DATABASE_URL; queries are slow or storage grows; you plan a schema migration.
Skip it when: you are setting up a new Neon backend; you need login or live queries.

# Make it a habit: Slow queries found and verified.

Each week your agent runs the read-only neon inspect db checks on your Lakebase Postgres branch: outliers, calls, seq-scans, unused-indexes, bloat and more. It names one query to fix, re-runs the same check after a change, and keeps the results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly health check (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** same check rerun. Hard checks: neon inspect db checks complete without error; the same check is re-run after any change; migrations use a direct URL without -pooler; no CREATE EXTENSION without your OK. On fail: notify, max 1 retries.
- **Memory:** inspect results log at `loops/neon-postgres-loop/log.md`. Read first: last week's check results and the query flagged.

## Steps

1. **Use existing URL.** Use the DATABASE_URL or .neon file that is already there instead of a new project.
2. **Run the checks.** Run the smallest relevant neon inspect db checks, or inspect_database through MCP.
3. **Name one query.** Pick one specific query and read its plan with EXPLAIN (ANALYZE, BUFFERS, PREFETCH, FILECACHE) when it is safe.
4. **Hand off generic work.** For index, schema or query rewrites, load postgres-best-practices and carry the evidence over.
5. **Test on a branch.** Test any migration on a branch of production over a direct connection.
6. **Verify the change.** Re-run the same check and workload and compare with the log.

Stop rule: Stops after one inspection pass and at most one query change per run.

## Permissions

- Writes: loops/neon-postgres-loop/**, migrations/**
- Network: neon.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/neon-postgres-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly health check. Verification: same check rerun. Memory: loops/neon-postgres-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
