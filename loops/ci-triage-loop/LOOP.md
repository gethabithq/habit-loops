---
name: cli-gh
title: GitHub CLI skill
repo: paulrberg/agent-skills
license: MIT
url: https://gethabit.dev/skills/paulrberg/cli-gh
---

# GitHub CLI skill

The github cli skill (cli-gh) helps agents use gh for repository reads, workflow runs, search, releases and configuration, with a bounded CI failure triage workflow.

- Install the skill: `npx skills add paulrberg/agent-skills --skill cli-gh`
- Source: https://github.com/paulrberg/agent-skills/tree/HEAD/skills/cli-gh
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A CI run fails; You need gh command syntax; You read repo data from the shell.
Skip it when: You write PRs or issues; You need to delete repositories.

# Make it a habit: Failing CI gets triaged fast.

When a CI run fails, your agent lists the failing runs with gh, pulls only the failed-step lines, checks toolchain drift against the workflow pins and, if you allowed fixes, pushes one and watches the new run. Causes go into a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** a CI run fails (event; GitHub Actions or Claude Code routine; `workflow_run.conclusion == failure`)
- **Verification:** new run passes. Hard checks: gh run watch --exit-status exits zero on the new run; the run URL comes back from gh run view --json url; local tool versions match the pins in .github/workflows/*.yml. On fail: notify, max 1 retries.
- **Memory:** CI failure log at `loops/ci-triage-loop/runs.md`. Read first: past failures with their causes and fixes.

## Steps

1. **Find failing runs.** gh run list with --status failure and --limit 5 lists failures for the branch or commit.
2. **Extract failed lines.** gh run view --log-failed, filtered with rg and head, keeps only error lines.
3. **Check toolchain drift.** Compare versions pinned in .github/workflows/*.yml with the local --version output.
4. **Fix the cause.** Only when you asked for fixes, the agent fixes the cause and pushes the commit.
5. **Watch the new run.** gh run watch with --exit-status follows the new run to the end.
6. **Report the result.** The run URL and final status go into the run log.

Stop rule: Stops after five failing runs and one fix attempt per run.

## Permissions

- Writes: loops/ci-triage-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ci-triage-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: a CI run fails. Verification: new run passes. Memory: loops/ci-triage-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
