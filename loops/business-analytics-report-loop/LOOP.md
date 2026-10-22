---
name: business-analytics-reporter
title: Business Analytics Reporter skill
repo: ailabs-393/ai-labs-claude-skills
license: MIT
url: https://gethabit.dev/skills/ailabs-393/business-analytics-reporter
---

# Business Analytics Reporter skill

The business analytics reporter skill helps business owners and analysts turn sales and revenue CSVs into a report that finds weak areas, explains the statistics and recommends improvement strategies.

- Install the skill: `npx skills add ailabs-393/ai-labs-claude-skills --skill business-analytics-reporter`
- Source: https://github.com/ailabs-393/ai-labs-claude-skills/tree/HEAD/dist/skills/business-analytics-reporter
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a business performance report; You analyze sales data from a CSV; You need improvement strategies.
Skip it when: Your data is not in CSV form; You need audited financial statements.

# Make it a habit: Monthly report on weak business areas.

Each month your agent runs the analysis script on the latest sales CSV, reads the JSON report, explains weak areas by severity, matches each to a strategy from the business frameworks reference and writes an HTML or markdown report. A log keeps last month's metrics.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly sales report (schedule; Claude Code routine or cron; `0 8 2 * *`)
- **Verification:** report built from script. Hard checks: scripts/analyze_business_data.py exits 0 and writes the JSON report; every weak area in the report has a strategy with actions and success metrics; report file exists. On fail: retry, max 1 retries.
- **Memory:** monthly metrics log at `loops/business-analytics-report-loop/run-log.md`. Read first: last month's growth rate, volatility and weak areas.

## Steps

1. **Load data.** Load the CSV with pandas and check columns and date range.
2. **Run analysis.** Run python scripts/analyze_business_data.py on the CSV to write the JSON report.
3. **Interpret.** Explain current state, weak areas, causes and impact in plain language.
4. **Recommend.** Use references/business_frameworks.md to write strategies with actions, timeline and metrics.
5. **Write report.** Fill assets/report_template.html or the markdown format and compare with last month.

Stop rule: Stops after one CSV and one report per run.

## Permissions

- Writes: business_report.html, loops/business-analytics-report-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/business-analytics-report-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly sales report. Verification: report built from script. Memory: loops/business-analytics-report-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
