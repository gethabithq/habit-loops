---
name: redis-observability
title: Redis Observability skill
repo: redis/agent-skills
license: MIT
url: https://gethabit.dev/skills/redis/redis-observability
---

# Redis Observability skill

The redis observability skill helps ops teams decide which Redis metrics to monitor and alert on, and which built-in commands like SLOWLOG, INFO and MEMORY DOCTOR to use during incident triage.

- Install the skill: `npx skills add redis/agent-skills --skill redis-observability`
- Source: https://github.com/redis/agent-skills/tree/HEAD/plugins/redis-development/skills/redis-observability
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You set up Redis alerts; Redis latency goes up; You profile a slow FT.SEARCH query.
Skip it when: You only need Redis security hardening; You do not run Redis.

# Make it a habit: Catch Redis trouble before users do.

Every hour your agent reads INFO, computes the hit ratio and compares memory, clients, blocked clients, rejected connections and last save against alert limits. When one trips it runs SLOWLOG GET 10 and MEMORY DOCTOR. A log keeps readings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** hourly health check (schedule; cron or Claude Code routine; `0 * * * *`)
- **Verification:** metrics within alert limits. Hard checks: used_memory is under 80% of maxmemory; hit ratio is 80% or higher; rejected_connections is 0; blocked_clients is not above 0 for two readings in a row. On fail: notify, max 0 retries.
- **Memory:** hourly readings log at `loops/redis-health-check-loop/run-log.md`. Read first: recent readings to spot spikes, drops and trends.

## Steps

1. **Read INFO.** Run INFO and pull memory, clients, ops per second, hits, misses and last save time.
2. **Compare.** Check each metric against its alert condition and the last readings.
3. **Triage.** If a limit trips, run SLOWLOG GET 10, MEMORY DOCTOR and CLIENT LIST.
4. **Log and notify.** Write the reading and send a short note when a check fails.

Stop rule: Stops after one reading and at most one triage per instance per run.

## Permissions

- Writes: loops/redis-health-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/redis-health-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: hourly health check. Verification: metrics within alert limits. Memory: loops/redis-health-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
