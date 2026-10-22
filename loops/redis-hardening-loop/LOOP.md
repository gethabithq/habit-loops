---
name: redis-security
title: Redis Security skill
repo: redis/agent-skills
license: MIT
url: https://gethabit.dev/skills/redis/redis-security
---

# Redis Security skill

The redis security skill helps ops and backend teams harden Redis for production with authentication, TLS, least-privilege ACL users, bind and protected-mode, firewall rules and disabled dangerous commands.

- Install the skill: `npx skills add redis/agent-skills --skill redis-security`
- Source: https://github.com/redis/agent-skills/tree/HEAD/plugins/redis-development/skills/redis-security
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You deploy Redis to production; A scanner reports exposed Redis; You define ACL users per app.
Skip it when: Redis runs only on your laptop; You use a fully managed Redis with fixed settings.

# Make it a habit: Redis stays locked down.

Each week and on every redis.conf change, your agent audits authentication, TLS, ACL users, bind and protected-mode, firewall rules and disabled dangerous commands together. A run log keeps the last audit so any regression stands out.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly Redis audit (schedule; Claude Code routine or cron; `0 5 * * 1`)
- **Verification:** hardening checklist passes. Hard checks: requirepass or ACL users are set; tls-port is configured; no bind 0.0.0.0 with protected-mode no; application ACL users exclude @dangerous; FLUSHALL, DEBUG and CONFIG are renamed or disabled. On fail: notify, max 0 retries.
- **Memory:** audit results log at `loops/redis-hardening-loop/run-log.md`. Read first: last audit result per instance.

## Steps

1. **Read config.** Read redis.conf for auth, TLS, bind, protected-mode and rename-command lines.
2. **Check ACLs.** Confirm each application has its own ACL user with only the commands and keys it needs.
3. **Check network.** Confirm firewall rules allow only application subnets on the Redis port.
4. **Compare.** Compare with the last audit and flag anything that got weaker.
5. **Report.** List gaps across all three areas, since one alone leaves a gap.

Stop rule: Stops after one Redis instance per run.

## Permissions

- Writes: loops/redis-hardening-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/redis-hardening-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly Redis audit. Verification: hardening checklist passes. Memory: loops/redis-hardening-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
