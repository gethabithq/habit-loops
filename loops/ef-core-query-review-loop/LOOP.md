---
name: optimizing-ef-core-queries
title: Optimizing EF Core Queries skill
repo: dotnet/skills
license: MIT
url: https://gethabit.dev/skills/dotnet/optimizing-ef-core-queries
---

# Optimizing EF Core Queries skill

The optimizing ef core queries skill reviews and fixes Entity Framework Core data access: N+1 queries, premature materialization, index-hostile predicates, tracking, Includes, paging, bulk writes and DbContext overlap. For .NET developers with slow data access.

- Install the skill: `npx skills add dotnet/skills --skill optimizing-ef-core-queries`
- Source: https://github.com/dotnet/skills/tree/HEAD/plugins/dotnet-data/skills/optimizing-ef-core-queries
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: EF Core queries are slow; You see N+1 query patterns; Deep pages get slower.
Skip it when: You use Dapper or raw ADO.NET; You have no data access code.

# Make it a habit: Catch slow EF Core queries early.

On each pull request touching data access, your agent traces every EF Core query to execution, counts database operations, checks materialization, predicates, tracking, Includes, paging, SaveChanges placement and DbContext overlap, and reports prioritized findings with safe fixes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** data access code changes (event; GitHub Actions or Claude Code routine; `pull request touches DbContext, repositories or queries`)
- **Verification:** findings with evidence. Hard checks: every finding names a location and call path; no migration applied with dotnet ef database update; tests pass. On fail: notify, max 0 retries.
- **Memory:** query finding log at `loops/ef-core-query-review-loop/findings.md`. Read first: open findings and queries flagged before.

## Steps

1. **Find the boundary.** Your agent finds the DbContext, DbSets, repositories and model-building code.
2. **Trace execution.** It follows each query to execution and checks Queryable versus Enumerable.
3. **Count operations.** It counts round-trips and SaveChanges calls on the calling path.
4. **Check each query.** It checks predicates, projections, bounds, ordering, Includes, tracking and parameterization.
5. **Report.** It lists prioritized findings with impact and a safe fix, and notes what was not validated.
6. **Ask on migrations.** For index fixes it adds a migration and asks you before any database update.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/ef-core-query-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ef-core-query-review-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: data access code changes. Verification: findings with evidence. Memory: loops/ef-core-query-review-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
