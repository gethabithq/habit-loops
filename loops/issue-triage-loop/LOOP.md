---
name: issue-triage
title: Issue Triage skill
repo: rtk-ai/rtk
license: Apache-2.0
url: https://gethabit.dev/skills/rtk-ai/issue-triage
---

# Issue Triage skill

The issue triage skill audits open GitHub issues with gh, categorizes them, finds likely duplicates, links PRs, rates risk and staleness, then drafts comments, labels and closes that it runs only after you approve. For maintainers with a large issue list.

- Install the skill: `npx skills add rtk-ai/rtk --skill issue-triage`
- Source: https://github.com/rtk-ai/rtk/tree/HEAD/.claude/skills/issue-triage
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Many issues have no triage; You suspect duplicate issues; You want stale issues cleaned up.
Skip it when: You only need a general repo recap; gh is not logged in.

# Make it a habit: Sort open issues, act after approval.

When issues pile up, your agent audits open issues with gh, sorts them by category, risk, linked PRs, likely duplicates and staleness, runs deep analysis on the ones you pick, drafts comments, labels and closes, and runs only the actions you approve.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** untriaged issues pile up (schedule; Claude Code routine; `manual /issue-triage, or more than 10 untriaged issues, or an issue stale over 30 days`)
- **Verification:** preconditions and your approval. Hard checks: git rev-parse --is-inside-work-tree succeeds; gh auth status succeeds; no label added twice; no close proposed for a collaborator's issue; no action run without your approval. On fail: stop, max 0 retries.
- **Memory:** triage tables at `loops/issue-triage-loop/triage.md`. Read first: last tables, duplicates and stale issues.

## Steps

1. **Check preconditions.** Your agent confirms the git repo and gh login, or stops.
2. **Gather data.** It lists open issues, open PRs, recently closed issues and collaborators with gh.
3. **Analyze.** It categorizes, links PRs, scores duplicates with Jaccard similarity, colors risk and marks stale issues.
4. **Show tables.** It prints critical, PR-linked, active, duplicate and stale tables and copies them to the clipboard.
5. **Deep analysis.** For issues you choose, parallel agents rate scope, missing info, effort and priority.
6. **Draft actions.** It drafts English comments from templates/issue-comment.md, plus labels or closes.
7. **Run on approval.** It asks which to run, then comments, labels and closes in that order.

Stop rule: Stops after one triage pass, at most 100 open issues listed.

## Permissions

- Writes: loops/issue-triage-loop/**
- Network: github.com
- Sends: GitHub issue comments, issue labels and closes
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/issue-triage-loop/triage.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: untriaged issues pile up. Verification: preconditions and your approval. Memory: loops/issue-triage-loop/triage.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
