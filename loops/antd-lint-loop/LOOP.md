---
name: antd
title: Ant Design (antd) skill
repo: ant-design/ant-design-cli
license: MIT
url: https://gethabit.dev/skills/ant-design/antd
---

# Ant Design (antd) skill

The Ant Design (antd) skill teaches agents the Ant Design CLI: query props, demos, tokens and docs offline, lint and analyze project usage, and follow migration guides between antd versions. For React developers using Ant Design.

- Install the skill: `npx skills add ant-design/ant-design-cli --skill antd`
- Source: https://github.com/ant-design/ant-design-cli/tree/HEAD/skills/antd
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write antd components; You migrate between antd versions; You debug an antd issue.
Skip it when: The project does not use antd; You use another UI library.

# Make it a habit: Keep antd usage current and clean.

On each pull request touching antd code, your agent runs antd lint on the changed files, checks props against your antd version with antd info, fixes deprecated usage and reruns lint. A board keeps usage stats from antd usage over time.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** antd code changes (event; GitHub Actions or Claude Code routine; `pull request touches files importing antd`)
- **Verification:** antd lint is clean. Hard checks: antd lint --format json reports no deprecated usage; antd doctor reports no configuration issues; build passes. On fail: retry, max 2 retries.
- **Memory:** antd usage board at `loops/antd-lint-loop/board.md`. Read first: last usage stats and open lint findings.

## Steps

1. **Check the CLI.** Your agent runs which antd and installs @ant-design/cli if missing.
2. **Match the version.** It reads your antd version and passes --version to queries.
3. **Lint.** It runs antd lint on changed files with --format json.
4. **Look up APIs.** For each finding it runs antd info and antd demo before fixing.
5. **Fix and relint.** It fixes deprecated or wrong usage and runs antd lint again.
6. **Track usage.** It runs antd usage on ./src and updates the board.

Stop rule: Stops after 15 files or 2 fix rounds per run.

## Permissions

- Writes: src/**, loops/antd-lint-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/antd-lint-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: antd code changes. Verification: antd lint is clean. Memory: loops/antd-lint-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
