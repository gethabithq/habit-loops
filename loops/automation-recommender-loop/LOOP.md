---
name: claude-automation-recommender
title: Claude Automation Recommender skill
repo: anthropics/claude-plugins-official
license: Apache-2.0
url: https://gethabit.dev/skills/anthropics/claude-automation-recommender
---

# Claude Automation Recommender skill

The claude automation recommender skill scans a codebase and suggests the most useful Claude Code hooks, subagents, skills, plugins and MCP servers for it, for developers setting up or tuning their agent workflow.

- Install the skill: `npx skills add anthropics/claude-plugins-official --skill claude-automation-recommender`
- Source: https://github.com/anthropics/claude-plugins-official/tree/HEAD/plugins/claude-code-setup/skills/claude-automation-recommender
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You first set up Claude Code for a project; You want to improve your agent workflow; You wonder which MCP servers fit your stack.
Skip it when: You want the automations built for you; You already know exactly which hook you need.

# Make it a habit: Fresh automation ideas every month.

Once a month your agent scans the codebase for its stack, tests, CI and existing Claude Code config, then recommends the top one or two hooks, subagents, skills, plugins and MCP servers. A log keeps past reports so only new ideas surface.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** first day each month (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** report shape check. Hard checks: report has a Codebase Profile section; at most 2 recommendations per category; each recommendation names a signal found in the codebase; no project files changed by the run. On fail: retry, max 1 retries.
- **Memory:** past recommendation reports at `loops/automation-recommender-loop/run-log.md`. Read first: recommendations already made and which ones now exist in .claude/ or .mcp.json.

## Steps

1. **Read past reports.** The agent reads the run log to see what it suggested before.
2. **Profile the codebase.** It detects language, framework, key libraries, tests, CI, issue tracking and existing .claude/ config.
3. **Match signals.** It maps each signal to MCP servers, skills, hooks, subagents and plugins using the skill's tables.
4. **Search for extras.** It uses web search for options specific to the detected tools and libraries.
5. **Pick the top ones.** It keeps one or two per category, skips irrelevant categories and drops ideas already set up.
6. **Write the report.** It writes the report in the skill's format and appends it to the run log without touching project files.

Stop rule: Stops after one report per run, at most 2 recommendations per category.

## Permissions

- Writes: loops/automation-recommender-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/automation-recommender-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: first day each month. Verification: report shape check. Memory: loops/automation-recommender-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
