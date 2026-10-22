---
name: logfire-query
title: Logfire Query skill
repo: pydantic/skills
license: MIT
url: https://gethabit.dev/skills/pydantic/logfire-query
---

# Logfire Query skill

Logfire query is a skill for developers who query and analyse Logfire telemetry with SQL: traces, logs, spans and metrics, through the MCP query_run tool or the REST /v1/query API.

- Install the skill: `npx skills add pydantic/skills --skill logfire-query`
- Source: https://github.com/pydantic/skills/tree/HEAD/plugins/logfire/skills/logfire-query
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You look up errors in Logfire; You find the slowest spans; You add query code to a project.
Skip it when: You want to open the Logfire UI; You do not use Logfire.

# Make it a habit: Daily summary of new errors.

Every morning, your agent queries Logfire for exceptions and slow spans from the last day, groups errors by service and compares them with yesterday's digest. Each query has a LIMIT and stays within the 14-day range.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** queries run with LIMIT. Hard checks: every SQL query has a LIMIT; time range is at most 14 days; query_run returns without error. On fail: retry, max 1 retries.
- **Memory:** daily error digests at `loops/logfire-error-digest-loop/run-log.md`. Read first: yesterday's error counts by service and top exception types.

## Steps

1. **Classify the route.** Treat the run as query analysis, not a Logfire UI view.
2. **Query errors.** Call query_run on the records table for rows where is_exception is true, with a LIMIT.
3. **Group by service.** Count errors per service_name and list top exception_type values.
4. **Find slow spans.** Query spans with long duration, ordered by duration, with a LIMIT.
5. **Compare and log.** Compare with yesterday's digest and write new or growing errors to the log.

Stop rule: Stops after five queries per run.

## Permissions

- Writes: loops/logfire-error-digest-loop/**
- Network: logfire-api.pydantic.dev, logfire-us.pydantic.dev, logfire-eu.pydantic.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/logfire-error-digest-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: queries run with LIMIT. Memory: loops/logfire-error-digest-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
