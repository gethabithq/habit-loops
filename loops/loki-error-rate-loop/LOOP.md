---
name: loki
title: Loki skill
repo: grafana/skills
license: Apache-2.0
url: https://gethabit.dev/skills/grafana/loki
---

# Loki skill

The loki skill covers Grafana Loki and the LogQL query language: stream selectors, line filters, parsers, metric queries, log ingestion and architecture. For engineers who write LogQL, run Loki or debug log pipelines.

- Install the skill: `npx skills add grafana/skills --skill loki`
- Source: https://github.com/grafana/skills/tree/HEAD/skills/grafana-lgtm/loki
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You write LogQL queries; You build an error rate alert; You set up log shipping with Alloy.
Skip it when: You do not use Grafana Loki; You need full-text search across all log content.

# Make it a habit: Log errors spotted every hour.

Every hour, your agent writes and runs LogQL queries against Grafana Loki: error rate by service, slow requests and 5xx errors. It compares the rate with an hour ago using offset, flags services over the threshold and logs the numbers.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every hour (schedule; Claude Code routine or cron; `0 * * * *`)
- **Verification:** queries run, threshold checked. Hard checks: every query starts with a log stream selector; the error rate query returns a value per service; services above 0.05 error rate are listed. On fail: notify, max 1 retries.
- **Memory:** hourly error rates at `loops/loki-error-rate-loop/log.md`. Read first: last error rates per service.

## Steps

1. **Select streams.** Your agent starts each query with a label selector such as env="prod".
2. **Filter early.** It puts line filters like |= "error" first for speed.
3. **Parse fields.** It uses json, logfmt or pattern parsers to read status and duration.
4. **Compute rates.** It runs sum(rate(...)) by service and compares with offset 1h.
5. **Find slow and 5xx.** It lists requests with duration > 1s and status >= 500.
6. **Log and flag.** It writes the rates to the log and flags services above the threshold.

Stop rule: Stops after five queries per run, with one retry per query.

## Permissions

- Writes: loops/loki-error-rate-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/loki-error-rate-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every hour. Verification: queries run, threshold checked. Memory: loops/loki-error-rate-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
