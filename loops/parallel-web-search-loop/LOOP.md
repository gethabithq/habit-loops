---
name: parallel-web-search
title: Parallel Web Search skill
repo: parallel-web/parallel-agent-skills
license: MIT
url: https://gethabit.dev/skills/parallel-web/parallel-web-search
---

# Parallel Web Search skill

The parallel web search skill runs parallel-cli search from the command line, saves the full results as JSON and writes an answer with an inline citation for every claim. For agents that need sourced answers without a search MCP tool.

- Install the skill: `npx skills add parallel-web/parallel-agent-skills --skill parallel-web-search`
- Source: https://github.com/parallel-web/parallel-agent-skills/tree/HEAD/skills/parallel-web-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you need sourced answers with links; you want results saved as JSON; no web search MCP tool is available.
Skip it when: the Parallel web_search MCP tool already works; you need deep, exhaustive research.

# Make it a habit: Cited web answers every morning.

Each weekday morning your agent runs parallel-cli search on a saved question, keeps the full results as JSON, checks the exit status and warnings, and writes an answer where every claim links a source. The run log keeps past questions and file paths.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every weekday morning (schedule; Claude Code routine or cron; `0 8 * * 1-5`)
- **Verification:** exit status and citations. Hard checks: parallel-cli exits with status zero and returns no API error; the results list in the -o JSON file is not empty; every claim in the answer links a URL found in the JSON file; the answer ends with a Sources section. On fail: notify, max 1 retries.
- **Memory:** past questions and files at `loops/parallel-web-search-loop/runs.md`. Read first: questions already searched, their JSON file paths and the last run's warnings.

## Steps

1. **Read the log.** The agent opens the run log to see which questions ran before and where their results live.
2. **Name the file.** It picks a short lowercase file name with hyphens that fits today's question.
3. **Search.** It calls parallel-cli search with the objective, a few -q keywords, --json, --max-results 10 and -o.
4. **Check the result.** It reads the saved JSON, then checks the exit status, API errors and warnings.
5. **Write the answer.** It leads with the finding and links each fact to a URL from the JSON.
6. **List sources.** It adds a Sources section, names the JSON file path and appends a line to the run log.

Stop rule: One question per run, with at most one refined retry when results are sparse.

## Permissions

- Writes: /tmp/*.json, loops/parallel-web-search-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/parallel-web-search-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every weekday morning. Verification: exit status and citations. Memory: loops/parallel-web-search-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
