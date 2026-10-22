---
name: mongodb-natural-language-querying
title: MongoDB Natural Language Querying skill
repo: mongodb/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/mongodb/mongodb-natural-language-querying
---

# MongoDB Natural Language Querying skill

Mongodb natural language querying turns plain-language questions into read-only MongoDB find queries or aggregation pipelines, using schema, indexes and sample documents from the MongoDB MCP server. For developers and analysts querying MongoDB.

- Install the skill: `npx skills add mongodb/agent-skills --skill mongodb-natural-language-querying`
- Source: https://github.com/mongodb/agent-skills/tree/HEAD/plugins/mongodb-atlas/skills/mongodb-natural-language-querying
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You need a MongoDB query; You translate SQL to MongoDB; You group or filter documents.
Skip it when: You optimize an existing query; You need Atlas Search or vector search.

# Make it a habit: Recurring data questions answered read-only.

Each week your agent answers your saved data questions against MongoDB: it fetches indexes, schema and a few sample documents through the MongoDB MCP server, validates fields, writes a find query or aggregation and notes missing indexes. Queries stay read-only and are logged.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly data questions (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** fields validated, read-only. Hard checks: every field in the query exists in the fetched schema; no query uses $where; no pipeline contains a write stage; each query returns a result count above zero or reports none. On fail: notify, max 1 retries.
- **Memory:** saved query log at `loops/mongodb-report-query-loop/log.md`. Read first: saved questions, the queries that answered them and index notes.

## Steps

1. **Load questions.** Read the saved questions and their database and collection names.
2. **Fetch context.** Call collection-indexes, collection-schema with a sample size and find with a small limit.
3. **Validate fields.** Check every field name and type against the schema before writing the query.
4. **Write the query.** Prefer a find query and use an aggregation only for grouping, joins or multi-stage work.
5. **Check indexes.** Note when no index supports the filter so you can decide whether to add one.
6. **Run and log.** Run the query through the MCP server and log the query and result summary.

Stop rule: Stops after at most 10 saved questions per run, with 1 retry each.

## Permissions

- Writes: loops/mongodb-report-query-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/mongodb-report-query-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly data questions. Verification: fields validated, read-only. Memory: loops/mongodb-report-query-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
