---
name: tavily-research
title: Tavily Research skill
repo: tavily-ai/skills
license: MIT
url: https://gethabit.dev/skills/tavily-ai/tavily-research
---

# Tavily Research skill

The tavily research skill runs deep, multi-source web research through the tvly CLI and returns a structured report with citations, for people who need comparisons, market analysis or literature reviews.

- Install the skill: `npx skills add tavily-ai/skills --skill tavily-research`
- Source: https://github.com/tavily-ai/skills/tree/HEAD/skills/tavily-research
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a cited research report; You compare products or vendors; You want a market or literature review.
Skip it when: You need one quick fact; You have no Tavily access.

# Make it a habit: A fresh cited report every week.

Every Monday your agent runs tavily research with the pro model on your standing topics, saves each JSON report with -o, checks it has citations and compares it with last week's report. It keeps a log of topics and report files.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Mondays at 07:00 (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** report saved with sources. Hard checks: tvly research exits without error; the -o output file exists; the report cites more than zero sources. On fail: retry, max 1 retries.
- **Memory:** research topics log at `loops/tavily-weekly-research-loop/run-log.md`. Read first: topics, last report files and what changed.

## Steps

1. **Read topics.** The agent reads the standing topics and last week's report paths from the log.
2. **Pick the model.** It uses mini for one narrow topic and pro for comparisons.
3. **Run research.** It runs tvly research with --json and -o for each topic.
4. **Handle long runs.** For slow topics it starts with --no-wait and fetches with tvly research poll.
5. **Compare.** It notes what is new against last week's report and updates the log.

Stop rule: Stops after at most 5 topics per run.

## Permissions

- Writes: loops/tavily-weekly-research-loop/**
- Network: Tavily via the tvly CLI
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/tavily-weekly-research-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Mondays at 07:00. Verification: report saved with sources. Memory: loops/tavily-weekly-research-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
