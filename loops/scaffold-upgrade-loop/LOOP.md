---
name: google-agents-cli-scaffold
title: Google Agents CLI Scaffold skill
repo: google/agents-cli
license: Apache-2.0
url: https://gethabit.dev/skills/google/google-agents-cli-scaffold
---

# Google Agents CLI Scaffold skill

The google agents cli scaffold skill by Google creates, enhances and upgrades agent projects with agents-cli scaffold: templates, deployment targets, CI/CD runners, session storage and the prototype-first pattern.

- Install the skill: `npx skills add google/agents-cli --skill google-agents-cli-scaffold`
- Source: https://github.com/google/agents-cli/tree/HEAD/skills/google-agents-cli-scaffold
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You start a new agent project; You add deployment or CI/CD; You upgrade a project template.
Skip it when: You write agent logic; You run a deployment.

# Make it a habit: Agent projects stay on current templates.

Each month your agent previews agents-cli scaffold upgrade with --dry-run, shows you the changes and applies them on your yes. Then it checks imports, runs the tests and a smoke prompt. A log keeps each upgrade and the files it changed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly template upgrade (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** your yes + tests. Hard checks: agents-cli scaffold upgrade --dry-run runs without error; the project's tests pass after the upgrade; agents-cli run answers a smoke prompt. On fail: stop, max 0 retries.
- **Memory:** upgrade log at `loops/scaffold-upgrade-loop/upgrades.md`. Read first: the last upgrade, files changed and any leftovers removed by hand.

## Steps

1. **Load the workflow.** Your agent loads google-agents-cli-workflow for the rules it must follow.
2. **Preview.** It runs agents-cli scaffold upgrade --dry-run to list the files that would change.
3. **Ask you.** It shows the changes and waits for your yes before applying them.
4. **Upgrade.** It runs agents-cli scaffold upgrade, and uses --force only when smart-merge fails.
5. **Clean up.** It lists files and dependencies the new template dropped, for you to remove by hand.
6. **Verify.** It checks imports, runs the tests and runs agents-cli run with a test prompt.
7. **Log.** It writes the version and changed files to the upgrade log.

Stop rule: Stops after one project upgrade per run.

## Permissions

- Writes: project scaffolding files, loops/scaffold-upgrade-loop/**
- Network: pypi.org
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/scaffold-upgrade-loop/upgrades.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly template upgrade. Verification: your yes + tests. Memory: loops/scaffold-upgrade-loop/upgrades.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
