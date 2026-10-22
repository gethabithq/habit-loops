---
name: bkt
title: bkt skill
repo: avivsinai/bitbucket-cli
license: MIT
url: https://gethabit.dev/skills/avivsinai/bkt
---

# bkt skill

The bkt skill helps developers operate Bitbucket Cloud or Data Center from the terminal: repositories, pull requests, branches, issues, pipelines, permissions and webhooks.

- Install the skill: `npx skills add avivsinai/bitbucket-cli --skill bkt`
- Source: https://github.com/avivsinai/bitbucket-cli/tree/HEAD/.agents/skills/bkt
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You manage Bitbucket pull requests from the CLI; You check pipeline or commit status; You script Bitbucket with JSON output.
Skip it when: Your code is on GitHub or GitLab; You need to store tokens in commands.

# Make it a habit: Failing Bitbucket PRs flagged daily.

Each workday your agent runs bkt auth status, confirms Cloud or Data Center, reads open pull requests and their commit statuses with --json output, and reports which PRs have failing checks, without making changes you did not request.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** workday PR check (schedule; Claude Code routine; `0 9 * * 1-5`)
- **Verification:** read-only report produced. Hard checks: bkt auth status succeeds; the report lists every open pull request; no create, merge, approve or delete command ran. On fail: notify, max 1 retries.
- **Memory:** daily PR report log at `loops/bitbucket-pr-status-loop/run-log.md`. Read first: PRs that were failing yesterday.

## Steps

1. **Check auth.** Run bkt auth status to find the active platform and context.
2. **Confirm platform.** Use Cloud or Data Center commands only for the active platform.
3. **Read PRs.** List open pull requests per rules/pr.md with --json output.
4. **Read checks.** Inspect commit and PR statuses per rules/status.md.
5. **Report.** List failing PRs with their URLs or identifiers.

Stop rule: Stops after 3 repositories per run.

## Permissions

- Writes: loops/bitbucket-pr-status-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/bitbucket-pr-status-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: workday PR check. Verification: read-only report produced. Memory: loops/bitbucket-pr-status-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
