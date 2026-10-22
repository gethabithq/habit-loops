---
name: langfuse
title: Langfuse skill
repo: langfuse/skills
license: MIT
url: https://gethabit.dev/skills/langfuse/langfuse
---

# Langfuse skill

The langfuse skill helps agents work with Langfuse: tracing, prompt management, datasets, experiments and evaluations, through langfuse-cli and the current docs. For teams who build and monitor AI applications.

- Install the skill: `npx skills add langfuse/skills --skill langfuse`
- Source: https://github.com/langfuse/skills/tree/HEAD/skills/langfuse
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You instrument an app with Langfuse tracing; You set up evals or datasets; You query Langfuse data from the command line.
Skip it when: You use a different observability tool; You have no AI application to trace.

# Make it a habit: Weekly failure modes from real traces.

Every week your agent reads current Langfuse docs, uses langfuse-cli to list recent data, runs an error analysis on the traces, and records the failure modes it finds. A run log keeps the modes so the next week compares against them.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly on Monday (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** data read, modes logged. Hard checks: LANGFUSE_PUBLIC_KEY, LANGFUSE_SECRET_KEY and LANGFUSE_BASE_URL are set; npx langfuse-cli api __schema returns resources; the list call returns a count above zero; the run log gains at least one entry. On fail: notify, max 1 retries.
- **Memory:** failure modes log at `loops/langfuse-trace-review-loop/run-log.md`. Read first: failure modes found in earlier weeks.

## Steps

1. **Read the log.** The agent reads the failure modes found in earlier weeks.
2. **Fetch current docs.** It reads llms.txt from langfuse.com and the pages it needs, never working from memory.
3. **Discover the API.** It runs npx langfuse-cli api __schema and the --help of the resource it needs.
4. **List recent data.** It uses list and get actions of langfuse-cli to read recent traces.
5. **Analyse errors.** It follows references/error-analysis.md to name concrete failure modes.
6. **Write the log.** It records the modes and suggests evals or dataset items from references/setting-up-evals.md.

Stop rule: Stops after one weekly review and at most 1 retry of a failed CLI call.

## Permissions

- Writes: loops/langfuse-trace-review-loop/**
- Network: langfuse.com, cloud.langfuse.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/langfuse-trace-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly on Monday. Verification: data read, modes logged. Memory: loops/langfuse-trace-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
