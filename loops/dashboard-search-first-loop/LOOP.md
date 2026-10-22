---
name: cx-search-dashboard
title: Dashboard Search skill
repo: coralogix/cx-cli
license: Apache-2.0
url: https://gethabit.dev/skills/coralogix/cx-search-dashboard
---

# Dashboard Search skill

Dashboard Search (the cx-search-dashboard skill) finds existing Coralogix dashboards and widgets by plain-language description or field path using the cx dashboards CLI, so you reuse rather than duplicate. For engineers managing Coralogix monitoring.

- Install the skill: `npx skills add coralogix/cx-cli --skill cx-search-dashboard`
- Source: https://github.com/coralogix/cx-cli/tree/HEAD/skills/cx-search-dashboard
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: checking whether a dashboard already exists; finding widgets that query a field; reusing existing query patterns.
Skip it when: you do not use Coralogix; you already know the dashboard you need.

# Make it a habit: No duplicate Coralogix dashboards built.

Before anyone builds a Coralogix dashboard, your agent searches existing dashboards and widgets with the cx dashboards CLI and reports matches. A run log keeps which topics were already covered.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new dashboard requested (event; Claude Code routine; `a dashboard build is asked for`)
- **Verification:** search returned results. Hard checks: cx dashboards search runs and exits with success; cx dashboards query-search returns a result set; a found dashboard's JSON is pulled with cx dashboards get. On fail: notify, max 1 retries.
- **Memory:** search log at `loops/dashboard-search-first-loop/run-log.md`. Read first: topics and fields already found to have dashboards.

## Steps

1. **Search by topic.** Your agent runs cx dashboards search with the service or topic in plain words.
2. **Search widgets.** It runs cx dashboards query-search with a description to find widgets whose queries fit.
3. **Search by field.** It runs cx dashboards query-search with a field path to see how that field is already queried.
4. **Try phrasings.** Since description search is fuzzy, it tries a few wordings when the first returns nothing.
5. **Inspect.** It pulls a matching dashboard with cx dashboards get -o json to study the query structure.
6. **Report.** It reports whether a dashboard already exists or the build is justified.

Stop rule: Stops after one search request per run, with at most one retry.

## Permissions

- Writes: loops/dashboard-search-first-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/dashboard-search-first-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new dashboard requested. Verification: search returned results. Memory: loops/dashboard-search-first-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
