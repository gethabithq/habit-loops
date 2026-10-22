---
name: planetscale-query-insights-and-tags
title: PlanetScale Query Insights and Tags skill
repo: planetscale/skills
license: MIT
url: https://gethabit.dev/skills/planetscale/planetscale-query-insights-and-tags
---

# PlanetScale Query Insights and Tags skill

Planetscale query insights and tags is a skill for database owners that reads PlanetScale Insights to find risky queries and recommends SQLCommenter tags, Traffic Control slices and schema or code fixes, applying nothing.

- Install the skill: `npx skills add planetscale/skills --skill planetscale-query-insights-and-tags`
- Source: https://github.com/planetscale/skills/tree/HEAD/planetscale-query-insights-and-tags
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to know what loads the database; Queries lack attribution tags; You plan Traffic Control budgets.
Skip it when: You do not use PlanetScale; You want changes applied automatically.

# Make it a habit: Weekly risky queries and tag gaps.

Every week, your agent reads PlanetScale Insights for top queries by time, rows, count, errors and anomalies, checks tag coverage and cardinality, and proposes tags, Traffic Control slices and code fixes. It changes nothing without approval.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly insights review (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** tables complete, no changes. Hard checks: the query risk table lists each top pattern; no recommended tag is in the never-default list; the report ends with the no-changes line. On fail: notify, max 0 retries.
- **Memory:** weekly risk tables at `loops/query-insights-review-loop/run-log.md`. Read first: last week's top patterns and tag gaps.

## Steps

1. **Read Insights.** Call /insights sorted by totalTime, rowsRead, count and errorCount for the window.
2. **Read anomalies.** Read /insights/anomalies and /insights/errors for moving patterns.
3. **Check tags.** Use /insights/tags and /insights/tags/summaries to see attribution and cardinality.
4. **Check raw collection.** Report the effective raw query collection state as a capability.
5. **Classify fixes.** Mark each pattern as tag, Traffic Control, schema or code candidate.
6. **Report.** List proposed changes needing approval and end with the no-changes line.

Stop rule: Stops after one branch and the top 20 query patterns per run.

## Permissions

- Writes: loops/query-insights-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/query-insights-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly insights review. Verification: tables complete, no changes. Memory: loops/query-insights-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
