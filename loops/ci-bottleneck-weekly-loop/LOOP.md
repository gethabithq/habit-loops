---
name: diagnosing-ci-and-merge-bottlenecks
title: Diagnosing CI and Merge Bottlenecks skill
repo: PostHog/skills
license: MIT
url: https://gethabit.dev/skills/posthog/diagnosing-ci-and-merge-bottlenecks
---

# Diagnosing CI and Merge Bottlenecks skill

The diagnosing ci and merge bottlenecks skill helps engineering teams use PostHog engineering analytics tools to find slow or flaky workflows, time to merge and stuck pull requests.

- Install the skill: `npx skills add PostHog/skills --skill diagnosing-ci-and-merge-bottlenecks`
- Source: https://github.com/PostHog/skills/tree/HEAD/skills/omnibus/diagnosing-ci-and-merge-bottlenecks
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ask whether CI is getting slower; You find where a PR is stuck; You measure time to merge.
Skip it when: You need a verdict on one CI failure; You want to save numbers as insights.

# Make it a habit: CI long pole named weekly.

Each week your agent compares workflow-health over two adjacent windows, finds the slow or flaky long-pole workflow, confirms its effect with pull-requests, opens one stuck PR with pr-lifecycle and reports median and p95 with honest caveats.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly CI health (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** numbers carry caveats. Hard checks: median and p95 are reported side by side; bots and drafts are excluded from merge-time stats; pending CI is never reported as a settled failure; truncated pull-requests results are flagged. On fail: notify, max 1 retries.
- **Memory:** CI health log at `loops/ci-bottleneck-weekly-loop/run-log.md`. Read first: last week's long pole and p95 values.

## Steps

1. **Pick the repo.** Call engineering-analytics-sources and pass source_id and repo on.
2. **Compare windows.** Call workflow-health for two adjacent windows and compare p50 and p95.
3. **Confirm on PRs.** Use pull-requests to list failing, pending and longest-open PRs.
4. **Open one PR.** Walk a stuck PR with pr-lifecycle and name the largest gap.
5. **Report.** Lead with a one-line verdict, then a short table with caveats.

Stop rule: Stops after one repo per run.

## Permissions

- Writes: loops/ci-bottleneck-weekly-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ci-bottleneck-weekly-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly CI health. Verification: numbers carry caveats. Memory: loops/ci-bottleneck-weekly-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
