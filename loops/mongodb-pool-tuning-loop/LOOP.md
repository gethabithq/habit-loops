---
name: mongodb-connection
title: MongoDB Connection skill
repo: mongodb/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/mongodb/mongodb-connection
---

# MongoDB Connection skill

The mongodb connection skill optimizes MongoDB client connection settings for any driver: pool sizes, timeouts and reuse patterns for serverless, OLTP, OLAP and bursty workloads, plus troubleshooting pool exhaustion and timeouts. For developers running MongoDB apps.

- Install the skill: `npx skills add mongodb/agent-skills --skill mongodb-connection`
- Source: https://github.com/mongodb/agent-skills/tree/HEAD/plugins/mongodb-atlas/skills/mongodb-connection
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You configure a MongoClient; You see pool exhaustion or timeouts; You build serverless functions on MongoDB.
Skip it when: The issue is DNS, VPC or TLS; You do not use MongoDB.

# Make it a habit: Size MongoDB connection pools from evidence.

When client setup changes or connection errors appear, your agent asks about deployment, workload and concurrency one question at a time, picks the matching scenario, sets pool and timeout values with a reason for each, and checks total connections against server limits.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** connection code or errors (event; Claude Code routine; `a change to MongoClient setup, or pool exhaustion and timeout errors`)
- **Verification:** sizing checks pass. Hard checks: maxPoolSize exceeds expected concurrency; instances x (maxPoolSize + 2) x members stays under the server limit; serverless clients are created outside the handler; each parameter has a written reason. On fail: retry, max 1 retries.
- **Memory:** pool settings log at `loops/mongodb-pool-tuning-loop/settings.md`. Read first: current settings, context answers and monitored numbers.

## Steps

1. **Gather context.** Your agent asks one question at a time about deployment, workload and concurrency.
2. **Classify the issue.** It separates client configuration issues from infrastructure issues and redirects the latter.
3. **Pick a scenario.** It matches serverless, OLTP, OLAP or bursty workloads.
4. **Size the pool.** It estimates pool size from ops per second and duration, or starts conservative.
5. **Check limits.** It counts total server connections including the 2 monitoring connections per member.
6. **Set up monitoring.** It points to references/monitoring-guide.md to track connections.current and wait queues.

Stop rule: Stops after one client config and one revision.

## Permissions

- Writes: src/**, loops/mongodb-pool-tuning-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/mongodb-pool-tuning-loop/settings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: connection code or errors. Verification: sizing checks pass. Memory: loops/mongodb-pool-tuning-loop/settings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
