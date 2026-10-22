---
name: mongodb-query-optimizer
title: MongoDB Query Optimizer skill
repo: mongodb/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/mongodb/mongodb-query-optimizer
---

# MongoDB Query Optimizer skill

The mongodb query optimizer skill helps agents find why MongoDB queries are slow and suggest indexes, using explain, collection indexes and Atlas Performance Advisor through MongoDB MCP. For developers tuning MongoDB performance.

- Install the skill: `npx skills add mongodb/agent-skills --skill mongodb-query-optimizer`
- Source: https://github.com/mongodb/agent-skills/tree/HEAD/plugins/mongodb-atlas/skills/mongodb-query-optimizer
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: A query is slow; You want index suggestions; You review slow queries on a cluster.
Skip it when: You only write a new query; You have no performance problem.

# Make it a habit: Suggest indexes for slow queries.

Each week your agent pulls slow query logs and index suggestions from Atlas Performance Advisor, checks the worst queries with explain and collection-indexes, and suggests indexes. You approve before any index is created. A board keeps suggestions.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly slow query review (schedule; Claude Code routine; `0 7 * * 1`)
- **Verification:** explain check, your approval. Hard checks: explain shows no COLLSCAN for the suggested index; collection stays at or under 20 indexes; no index created without your approval. On fail: notify, max 0 retries.
- **Memory:** index suggestion board at `loops/mongodb-slow-query-loop/board.md`. Read first: suggestions already made and which you approved.

## Steps

1. **Load references.** Your agent reads references/core-indexing-principles.md and references/antipattern-examples.md.
2. **Fetch slow queries.** It calls atlas-list-projects, then atlas-get-performance-advisor with slowQueryLogs and suggestedIndexes.
3. **Inspect top queries.** For the slowest and most frequent, it calls collection-indexes, explain and find.
4. **Diagnose.** It compares documents scanned with documents returned and looks for in-memory sorts.
5. **Suggest.** It suggests the highest-impact indexes with short reasons, as suggestions.
6. **Ask before creating.** It creates an index only after you approve.

Stop rule: Stops after the 5 slowest queries per run.

## Permissions

- Writes: loops/mongodb-slow-query-loop/**
- Network: mongodb.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/mongodb-slow-query-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly slow query review. Verification: explain check, your approval. Memory: loops/mongodb-slow-query-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
