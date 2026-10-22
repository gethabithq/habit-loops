---
name: groundcover-cli
title: Groundcover CLI skill
repo: paymog/groundcover-cli
license: MIT
url: https://gethabit.dev/skills/paymog/groundcover-cli
---

# Groundcover CLI skill

Groundcover cli lets an agent drive the groundcover command to query logs, traces, metrics and k8s events and to manage dashboards, monitors, silences and pipelines on Groundcover. For engineers debugging production with Groundcover.

- Install the skill: `npx skills add paymog/groundcover-cli --skill groundcover-cli`
- Source: https://github.com/paymog/groundcover-cli/tree/HEAD/skills/groundcover-cli
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You debug a production error; You check latency or crashlooping pods; You edit Groundcover dashboards or monitors.
Skip it when: You do not use Groundcover; You only have an ingestion key.

# Make it a habit: Production issues triaged with evidence.

Every morning your agent runs the groundcover triage flow for your key services: error logs, slow traces, PromQL error rate and latency, and k8s warning events and restarts. It writes a short triage note and keeps a log to compare day to day.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every weekday morning (schedule; Claude Code routine or cron; `0 8 * * 1-5`)
- **Verification:** all queries answered. Hard checks: groundcover auth status resolves a gcsa_ key; logs search, traces search and metrics query return without an error; the triage note lists each checked service. On fail: retry, max 1 retries.
- **Memory:** daily triage log at `loops/groundcover-prod-triage-loop/log.md`. Read first: yesterday's error counts and open issues.

## Steps

1. **Check auth.** Confirm groundcover auth status shows a valid gcsa_ service-account key.
2. **Set the window.** Compute start and end times in UTC with date -u, last hour by default.
3. **Logs first.** Run groundcover logs search with a GCQL filter on service_name and error level.
4. **Traces if slow.** Run groundcover traces search on duration_ms and pivot trace IDs back to logs.
5. **Metrics shape.** Use groundcover metrics query with PromQL range queries for error rate and p99.
6. **Is it running.** Check groundcover k8s workloads for restarts and k8s events-search for Warning events.
7. **Write the note.** Summarize findings per service and add them to the log.

Stop rule: Stops after five services per run and one retry per query.

## Permissions

- Writes: loops/groundcover-prod-triage-loop/**
- Network: api.groundcover.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/groundcover-prod-triage-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every weekday morning. Verification: all queries answered. Memory: loops/groundcover-prod-triage-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
