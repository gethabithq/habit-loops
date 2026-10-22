---
name: data-analyst
title: Data Analyst skill
repo: cline/skills
license: Apache-2.0
url: https://gethabit.dev/skills/cline/data-analyst
---

# Data Analyst skill

The data analyst skill helps teams ask questions of ClickHouse data the way an analyst would: clarify intent, resolve definitions, run safe bounded SQL with clickhousectl, then report with caveats.

- Install the skill: `npx skills add cline/skills --skill data-analyst`
- Source: https://github.com/cline/skills/tree/HEAD/skills/data-analyst
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You ask about active users or revenue; You need a funnel or trend from ClickHouse; You want a chart or data export.
Skip it when: Your data is not in ClickHouse; You only need a raw table dump.

# Make it a habit: Weekly metrics with clear definitions.

Each week your agent reruns your confirmed metric questions against ClickHouse with clickhousectl: it restates the saved intent block, checks the connection, runs bounded SQL, analyzes trends and reports answer, method, SQL and caveats. New ambiguity goes back to you.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly metrics report (schedule; Claude Code routine; `0 7 * * 1`)
- **Verification:** intent confirmed, answer shaped. Hard checks: no intent field is still NEED FROM USER before querying; every query ran through clickhousectl, not ClickHouse MCP tools; each answer has Answer, How I measured it, SQL/source and Caveats; artifact paths for saved CSVs or charts exist. On fail: stop, max 0 retries.
- **Memory:** confirmed intent blocks at `loops/clickhouse-metrics-report-loop/intents.md`. Read first: confirmed metric, population, window, grain and filters per question.

## Steps

1. **Restate intent.** Fill the intent block from the saved definitions and ask you about any new gap.
2. **Verify connection.** Load skills/clickhouse/ and confirm the right local server or Cloud service.
3. **Resolve terms.** Use skills/reading-data-dict/ for any LOOK UP term.
4. **Run bounded SQL.** Run previews and aggregates with clickhousectl, using skills/clickhouse-best-practices/ for complex SQL.
5. **Analyze.** Use skills/analyzer/ for trends, comparisons and sanity checks.
6. **Save and report.** Use skills/plotting/ and skills/artifact-management/, then write the standard answer.

Stop rule: Stops after 5 metric questions per run; asks before any unbounded or long query.

## Permissions

- Writes: loops/clickhouse-metrics-report-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/clickhouse-metrics-report-loop/intents.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly metrics report. Verification: intent confirmed, answer shaped. Memory: loops/clickhouse-metrics-report-loop/intents.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
