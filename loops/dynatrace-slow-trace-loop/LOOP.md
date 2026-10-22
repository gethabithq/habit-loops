---
name: dt-obs-tracing
title: DT Obs Tracing skill
repo: dynatrace/dynatrace-for-ai
license: Apache-2.0
url: https://gethabit.dev/skills/dynatrace/dt-obs-tracing
---

# DT Obs Tracing skill

The dt obs tracing skill analyses Dynatrace distributed traces and spans with DQL: slow requests, failed spans, failure reasons, service dependencies and exceptions, for SRE and backend teams.

- Install the skill: `npx skills add dynatrace/dynatrace-for-ai --skill dt-obs-tracing`
- Source: https://github.com/dynatrace/dynatrace-for-ai/tree/HEAD/skills/dt-obs-tracing
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: finding slow requests; analysing failed spans; mapping service dependencies.
Skip it when: log searching; DAVIS problem analysis.

# Make it a habit: Slow and failed requests found daily.

Every morning, your agent queries fetch spans for root requests over 5 seconds, failure rates by service and failure reasons, with exemplar trace IDs. Percentiles per endpoint are compared with the last run in a log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine; `0 8 * * *`)
- **Verification:** query rules hold. Hard checks: queries filter request.is_root_span == true; every listed slow request has a trace.id; operation counts use multiplicity extrapolation; duration is compared as a DQL duration such as 5s. On fail: retry, max 2 retries.
- **Memory:** endpoint latency log at `loops/dynatrace-slow-trace-loop/log.md`. Read first: p95 and p99 per endpoint from the last run.

## Steps

1. **Find slow requests.** Your agent lists root spans with duration over 5s in the last two hours.
2. **Rank endpoints.** It computes p95 and p99 per endpoint.name.
3. **Summarise failures.** It computes failure rate per dt.service.name.
4. **Explain failures.** It breaks failures down by reason, such as http_code or exception.
5. **Attach exemplars.** It adds trace IDs with takeAny(record(start_time, trace.id)) for drilldown.
6. **Compare and log.** It compares percentiles with the last run and writes changes to the log.

Stop rule: Stops after one report per run, with at most 50 slow traces listed.

## Permissions

- Writes: loops/dynatrace-slow-trace-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/dynatrace-slow-trace-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: query rules hold. Memory: loops/dynatrace-slow-trace-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
