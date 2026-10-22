---
name: rtk-triage
title: RTK Triage skill
repo: rtk-ai/rtk
license: Apache-2.0
url: https://gethabit.dev/skills/rtk-ai/rtk-triage
---

# RTK Triage skill

The rtk triage skill runs issue and PR triage together and cross-checks them for duplicate coverage, security gaps, critical bugs without PRs and conflicting internal PRs, saving a dated report. For maintainers of busy repos.

- Install the skill: `npx skills add rtk-ai/rtk --skill rtk-triage`
- Source: https://github.com/rtk-ai/rtk/tree/HEAD/.claude/skills/rtk-triage
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your PR and issue backlog grows fast; You plan a sprint; You want to find duplicate PRs.
Skip it when: The repo has few open items; You do not use gh.

# Make it a habit: Weekly cross-check of issues and PRs.

Each week your agent gathers open issues and PRs with gh, runs the issue-triage and pr-triage analyses, then cross-checks for double coverage, security gaps, P0 and P1 bugs without PRs and dirty internal PRs, and saves a dated report to claudedocs/.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly triage (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** report saved, no auto-posts. Hard checks: claudedocs/RTK-YYYY-MM-DD.md exists; report has all cross-analysis sections and the summary table; no GitHub comment posted without your approval. On fail: notify, max 1 retries.
- **Memory:** dated triage reports at `claudedocs/RTK-YYYY-MM-DD.md`. Read first: last week's report and its priority actions.

## Steps

1. **Check preconditions.** Your agent runs git rev-parse --is-inside-work-tree, gh auth status and date.
2. **Gather data.** It runs gh issue list and gh pr list, and gh pr view per PR for changed files.
3. **Triage each side.** It applies issue-triage and pr-triage logic for category, risk, size, CI and overlaps.
4. **Cross-check.** It finds double coverage, security findings without PRs, P0 and P1 bugs without PRs and dirty internal PRs.
5. **Summarize.** It prints the counted summary table.
6. **Save and ask.** It saves the report and asks you before posting any GitHub comment.

Stop rule: Stops after one report covering up to 200 issues and 200 PRs per run.

## Permissions

- Writes: claudedocs/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`claudedocs/RTK-YYYY-MM-DD.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly triage. Verification: report saved, no auto-posts. Memory: claudedocs/RTK-YYYY-MM-DD.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
