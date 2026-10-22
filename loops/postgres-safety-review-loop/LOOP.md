---
name: planetscale-postgres-safety-review
title: PlanetScale Postgres Safety Review skill
repo: planetscale/skills
license: MIT
url: https://gethabit.dev/skills/planetscale/planetscale-postgres-safety-review
---

# PlanetScale Postgres Safety Review skill

Planetscale postgres safety review is a skill for database owners that reviews PlanetScale Postgres roles, pg_strict, Traffic Control, query tags, backups and PITR, network posture and webhooks, without applying changes.

- Install the skill: `npx skills add planetscale/skills --skill planetscale-postgres-safety-review`
- Source: https://github.com/planetscale/skills/tree/HEAD/planetscale-postgres-safety-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit a PlanetScale Postgres database; Agents query your production database; You plan backups and restore drills.
Skip it when: You use PlanetScale Vitess; You want changes applied directly.

# Make it a habit: Postgres safety gaps found, nothing changed.

Each month, your agent reviews a PlanetScale Postgres database: branch workflow, roles, pg_strict, Query Insights, query tags, Traffic Control, backups, connections, extensions and webhooks. It proposes changes for approval and applies none.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly safety review (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** full review, no changes. Hard checks: the report covers every output section the skill lists; every proposed change is marked as needing approval; the report ends with: No Postgres changes have been applied.. On fail: notify, max 0 retries.
- **Memory:** last safety posture at `loops/postgres-safety-review-loop/posture.md`. Read first: last month's highest-risk gaps and proposals.

## Steps

1. **Check branches.** Check for a test branch, tested migrations and a documented rollback path.
2. **Check roles.** Flag use of the default role and check pg_strict on application roles.
3. **Review Insights.** Review slow, high-CPU, erroring queries, anomalies and the effective raw query setting.
4. **Check tags and budgets.** Check SQLCommenter tags and recommend Traffic Control budgets in warn mode.
5. **Check recovery and network.** Check backups, PITR, restore drills, pooling, private connectivity and IP restrictions.
6. **Check extensions and webhooks.** Review safety extensions and recommend webhooks such as branch.anomaly.
7. **Report.** List proposed changes needing approval and end with the no-changes line.

Stop rule: Stops after one database per run; no changes applied.

## Permissions

- Writes: loops/postgres-safety-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/postgres-safety-review-loop/posture.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly safety review. Verification: full review, no changes. Memory: loops/postgres-safety-review-loop/posture.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
