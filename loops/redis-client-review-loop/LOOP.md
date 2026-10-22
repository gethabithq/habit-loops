---
name: redis-connections
title: Redis Connections skill
repo: redis/agent-skills
license: MIT
url: https://gethabit.dev/skills/redis/redis-connections
---

# Redis Connections skill

The redis connections skill gives developers client-side guidance for Redis: connection pools or multiplexing, pipelining, SCAN instead of KEYS, RESP3 client-side caching and sensible connect and read timeouts.

- Install the skill: `npx skills add redis/agent-skills --skill redis-connections`
- Source: https://github.com/redis/agent-skills/tree/HEAD/skills/redis-connections
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: setting up a Redis client; many small Redis calls feel slow; iterating large keyspaces.
Skip it when: you need server-side Redis tuning; you do not use Redis.

# Make it a habit: Redis clients stay pooled and fast.

When a pull request touches Redis client code, your agent reviews it against the redis connections guidance: pooling or multiplexing, pipelines, SCAN instead of KEYS, timeouts. It logs each finding so the next review starts from known issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches Redis code (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize, files using a Redis client`)
- **Verification:** pattern checks plus tests. Hard checks: no KEYS pattern call in changed code; no new connection created per request; every BLPOP or BRPOP passes a timeout; connect timeout is set and shorter than read timeout; tests pass. On fail: notify, max 1 retries.
- **Memory:** Redis review log at `loops/redis-client-review-loop/log.md`. Read first: open findings from earlier reviews and files already fixed.

## Steps

1. **Read the diff.** The agent lists every changed file that sets up or calls a Redis client such as redis-py, Jedis or Lettuce.
2. **Check connection style.** It confirms the code uses a pool like ConnectionPool or one multiplexed connection, never a fresh connection per call.
3. **Spot batching chances.** Loops of independent commands get a suggestion to send them through a pipeline instead.
4. **Flag full scans.** Calls to KEYS, SMEMBERS, HGETALL or LRANGE 0 -1 on big data get swapped for SCAN, SSCAN, HSCAN or paging.
5. **Review timeouts.** It checks that socket_connect_timeout and socket_timeout are set and that blocking commands carry a timeout.
6. **Consider client caching.** For hot keys that rarely change, it suggests RESP3 client-side caching; for write-heavy data it advises against it.
7. **Log and report.** Findings go into the run log and a review comment, and tests run on the result.

Stop rule: Stops after one pull request and at most 20 findings per run.

## Permissions

- Writes: loops/redis-client-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/redis-client-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches Redis code. Verification: pattern checks plus tests. Memory: loops/redis-client-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
