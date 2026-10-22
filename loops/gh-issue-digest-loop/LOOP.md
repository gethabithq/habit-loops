---
name: gh
title: gh skill
repo: cli/cli
license: MIT
url: https://gethabit.dev/skills/cli/gh
---

# gh skill

Gh skill gives agents patterns for the GitHub CLI: JSON output, pagination limits, repo targeting, search versus list, sub-issues, attachments, discussions and gh api fallback. For developers whose agents work with GitHub from the terminal.

- Install the skill: `npx skills add cli/cli --skill gh`
- Source: https://github.com/cli/cli/tree/HEAD/skills/gh
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: An agent queries GitHub issues; You need structured gh output; You script PR or issue work.
Skip it when: You use the GitHub web UI only; You work on GitLab or Bitbucket.

# Make it a habit: Open issues and PRs summarized daily.

Each morning your agent checks gh auth status, then lists new issues, PRs waiting for review and blocked issues with gh search and gh issue list using --json and -L. It compares against yesterday and writes a short digest.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily repo digest (schedule; Claude Code routine or GitHub Actions; `0 8 * * 1-5`)
- **Verification:** auth + JSON results. Hard checks: gh auth status --json reports an active host; every gh call returns valid JSON; no list result equals its -L cap without a note about truncation. On fail: notify, max 1 retries.
- **Memory:** digest log at `loops/gh-issue-digest-loop/log.md`. Read first: issue and PR numbers reported yesterday.

## Steps

1. **Check auth.** Run gh auth status --json and ask you to log in again if the refresh expired.
2. **List new issues.** Run gh issue list with --json, --search and -L for issues opened since the last run.
3. **Find waiting PRs.** Run gh search prs with bare qualifiers like is:open for PRs waiting for review.
4. **Check blockers.** Read blockedBy and subIssues fields and compare node counts with totalCount.
5. **Write the digest.** List only what changed since yesterday and log the numbers.

Stop rule: Stops after one digest per run, with at most 100 items per list.

## Permissions

- Writes: loops/gh-issue-digest-loop/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gh-issue-digest-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily repo digest. Verification: auth + JSON results. Memory: loops/gh-issue-digest-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
