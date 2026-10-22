---
name: planetscale-best-practices-matrix
title: PlanetScale Best Practices Matrix skill
repo: planetscale/skills
license: MIT
url: https://gethabit.dev/skills/planetscale/planetscale-best-practices-matrix
---

# PlanetScale Best Practices Matrix skill

Planetscale best practices matrix is a skill for database owners that maps findings to PlanetScale safety, observability and automation features by engine, from Query Insights and webhooks to safe migrations and pg_strict.

- Install the skill: `npx skills add planetscale/skills --skill planetscale-best-practices-matrix`
- Source: https://github.com/planetscale/skills/tree/HEAD/planetscale-best-practices-matrix
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit a PlanetScale database; You plan safety features; You set agent rules for a database.
Skip it when: You do not use PlanetScale; You want changes applied automatically.

# Make it a habit: Find missing database safety features.

Each quarter, your agent walks the PlanetScale best-practices matrix for your engine, marks each feature as applies yes, no or unknown with its current state, gap and measured value, and ends without changing anything.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** quarterly database review (schedule; Claude Code routine; `0 9 1 */3 *`)
- **Verification:** matrix fully marked. Hard checks: every matrix item has applies yes, no or unknown; every gap has a recommendation ID and approval need; the report ends with: No changes have been applied.. On fail: notify, max 0 retries.
- **Memory:** last matrix review at `loops/planetscale-feature-gap-loop/matrix.md`. Read first: last quarter's gaps and their status.

## Steps

1. **Pick the engine.** Choose the Vitess or Postgres sections plus the cross-engine items.
2. **Check Insights.** Review slow, expensive and erroring query patterns in Query Insights.
3. **Walk the matrix.** Mark each item, such as webhooks, safe migrations or pg_strict, with state and gap.
4. **Quantify value.** Tie each gap to a measured finding, such as a query fingerprint or anomaly count.
5. **Mark approvals.** Note that humans approve database changes and agents only propose them.
6. **Close the report.** End with the line stating no changes have been applied.

Stop rule: Stops after one database per run; no changes applied.

## Permissions

- Writes: loops/planetscale-feature-gap-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/planetscale-feature-gap-loop/matrix.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: quarterly database review. Verification: matrix fully marked. Memory: loops/planetscale-feature-gap-loop/matrix.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
