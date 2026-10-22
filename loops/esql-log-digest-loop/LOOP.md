---
name: elasticsearch-esql
title: Elasticsearch ES|QL skill
repo: elastic/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/elastic/elasticsearch-esql
---

# Elasticsearch ES|QL skill

Elasticsearch ES|QL runs queries through the elastic CLI: it checks the cluster, discovers the schema, picks the right ES|QL feature and runs the simplest correct query for logs, metrics, search or time series. For engineers querying Elasticsearch.

- Install the skill: `npx skills add elastic/agent-skills --skill elasticsearch-esql`
- Source: https://github.com/elastic/agent-skills/tree/HEAD/plugins/elasticsearch/skills/elasticsearch-esql
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You analyze logs in Elasticsearch; You aggregate metrics over time; You look for spikes or patterns.
Skip it when: You need Query DSL JSON; Your cluster is older than 8.11.

# Make it a habit: Daily log patterns and spikes reported.

Each morning your agent checks the cluster with elastic es info, discovers the log index mapping, then runs ES|QL queries for error counts, CATEGORIZE patterns and CHANGE_POINT spikes over the last day. It writes a TSV-based digest and logs the queries that worked.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily log digest (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** connection + query runs. Hard checks: elastic es info returns a build_flavor; every query ran without an Elasticsearch error; every exploratory query ends with LIMIT. On fail: notify, max 2 retries.
- **Memory:** query and digest log at `loops/esql-log-digest-loop/log.md`. Read first: index names, field names and working queries from earlier runs.

## Steps

1. **Check the cluster.** Run elastic es info and use build_flavor and version to decide which features are available.
2. **Discover the schema.** List indices with elastic es cat indices and read the mapping, never guessing names.
3. **Pick features.** Use STATS for counts, CATEGORIZE for patterns and CHANGE_POINT for spikes where the license allows.
4. **Run queries.** Run each query with elastic es esql query --format tsv and fix errors from the message.
5. **Write the digest.** Summarize error counts, top patterns and detected change points and log the queries.

Stop rule: Stops after at most 5 queries per run, with 2 fixes per failing query.

## Permissions

- Writes: loops/esql-log-digest-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/esql-log-digest-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily log digest. Verification: connection + query runs. Memory: loops/esql-log-digest-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
