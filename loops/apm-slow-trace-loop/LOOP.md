---
name: dd-apm
title: Datadog APM skill
repo: datadog-labs/agent-skills
license: MIT
url: https://gethabit.dev/skills/datadog-labs/dd-apm
---

# Datadog APM skill

The datadog apm skill helps engineers set up Datadog APM on Kubernetes or Linux, search traces, analyze services and dependencies, and enable Data Streams Monitoring.

- Install the skill: `npx skills add datadog-labs/agent-skills --skill dd-apm`
- Source: https://github.com/datadog-labs/agent-skills/tree/HEAD/dd-apm
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You instrument services with SSI; You search slow or failing traces; You check service dependencies.
Skip it when: You do not use Datadog; You only need log search.

# Make it a habit: Slow and failing services flagged daily.

Each workday your agent confirms the env tag, lists services and stats with pup apm services, searches error and slow traces over the last hour with pup traces search, and reports the services that got worse.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily trace check (schedule; Claude Code routine; `0 9 * * 1-5`)
- **Verification:** services checked, env confirmed. Hard checks: pup apm services list returns more than zero services; every flagged service has an example trace query; the env tag was confirmed, not assumed. On fail: notify, max 1 retries.
- **Memory:** trace check log at `loops/apm-slow-trace-loop/run-log.md`. Read first: services flagged on earlier days.

## Steps

1. **Confirm env.** Ask you to confirm the env tag instead of assuming prod.
2. **List services.** Run pup apm services list and pup apm services stats for the last hour.
3. **Search errors.** Run pup traces search with status:error per service.
4. **Search slow traces.** Run pup traces search with @duration:>1000ms per service.
5. **Check dependencies.** Use pup apm flow-map for services that got worse.
6. **Report.** List flagged services with queries and fixes from the troubleshooting table.

Stop rule: Stops after 10 services per run.

## Permissions

- Writes: loops/apm-slow-trace-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/apm-slow-trace-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily trace check. Verification: services checked, env confirmed. Memory: loops/apm-slow-trace-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
