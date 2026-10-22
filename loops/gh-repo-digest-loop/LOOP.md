---
name: gh-cli
title: GitHub CLI skill
repo: logicrw/gh-cli-skill
license: MIT
url: https://gethabit.dev/skills/logicrw/gh-cli
---

# GitHub CLI skill

The github cli skill helps agents and developers do GitHub work with the gh command: pull requests, issues, code search, releases and API calls, with compact --json and --jq output.

- Install the skill: `npx skills add logicrw/gh-cli-skill --skill gh-cli`
- Source: https://github.com/logicrw/gh-cli-skill/tree/HEAD/gh-cli
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You work with PRs or issues; You search code on GitHub; You call the GitHub API from the shell.
Skip it when: You do not use GitHub; gh is not installed or authenticated.

# Make it a habit: A daily digest of your repo.

Each morning your agent uses gh with --json and --jq to list open PRs, their CI checks, new issues and the latest release, and writes a short digest of what changed since yesterday. A log keeps the last digest.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily repo digest (schedule; Claude Code routine or cron; `0 8 * * 1-5`)
- **Verification:** gh calls succeed. Hard checks: gh auth status passes; every gh call uses --json with selected fields; digest file exists. On fail: notify, max 1 retries.
- **Memory:** daily digest log at `loops/gh-repo-digest-loop/run-log.md`. Read first: yesterday's open PRs and issues.

## Steps

1. **Check auth.** Run gh auth status.
2. **List PRs.** Run gh pr list with --json number,title,author,updatedAt.
3. **Check CI.** Run gh pr checks for each open PR.
4. **List issues.** Run gh issue list with --json number,title,labels,assignees.
5. **Write digest.** Compare with yesterday and write what is new, stale or failing.

Stop rule: Stops after one repository and 50 items per run; read-only, no merges or comments.

## Permissions

- Writes: loops/gh-repo-digest-loop/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gh-repo-digest-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily repo digest. Verification: gh calls succeed. Memory: loops/gh-repo-digest-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
