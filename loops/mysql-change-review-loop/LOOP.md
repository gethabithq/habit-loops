---
name: mysql
title: MySQL skill
repo: planetscale/database-skills
license: MIT
url: https://gethabit.dev/skills/planetscale/mysql
---

# MySQL skill

Mysql helps an agent plan and review MySQL and InnoDB schema, indexes, queries, transactions and operations with measured evidence, small changes and rollback plans. For developers and DBAs changing MySQL databases.

- Install the skill: `npx skills add planetscale/database-skills --skill mysql`
- Source: https://github.com/planetscale/database-skills/tree/HEAD/skills/mysql
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add or change MySQL tables; You chase a slow or locking query; You plan a production migration.
Skip it when: You use Postgres or another database; You need no schema or query change.

# Make it a habit: Safe, measured MySQL changes.

When a pull request touches MySQL schema, indexes or queries, your agent defines the workload, reads only the matching references, proposes the smallest change, backs it with EXPLAIN evidence and adds rollback steps. Destructive operations wait for a human yes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes SQL (event; GitHub Actions or Claude Code routine; `pull_request touches migrations or queries`)
- **Verification:** EXPLAIN evidence, human yes. Hard checks: EXPLAIN output shows no type: ALL on changed queries; production changes include rollback and post-deploy verification steps; drops, deletes and truncates have explicit human approval. On fail: notify, max 0 retries.
- **Memory:** review notes at `loops/mysql-change-review-loop/notes.md`. Read first: past changes, their evidence and MySQL version notes.

## Steps

1. **Define the workload.** Note read/write mix, latency target, data volume, MySQL version and hosting.
2. **Read references.** Open only the reference files for the area at hand, such as indexes or locking.
3. **Propose small change.** Suggest the smallest fix that solves the problem, with trade-offs.
4. **Show evidence.** Validate with EXPLAIN or EXPLAIN ANALYZE and lock or connection metrics.
5. **Plan rollout.** For production, add online DDL where possible, rollback and post-deploy checks.
6. **Ask before deletes.** Get explicit human approval for any drop, delete or truncate.

Stop rule: Stops after one pull request per run; no retries on destructive steps.

## Permissions

- Writes: loops/mysql-change-review-loop/**
- Network: raw.githubusercontent.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/mysql-change-review-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes SQL. Verification: EXPLAIN evidence, human yes. Memory: loops/mysql-change-review-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
