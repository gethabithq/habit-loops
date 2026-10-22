---
name: claude-md-improver
title: CLAUDE.md Improver skill
repo: anthropics/claude-plugins-official
license: Apache-2.0
url: https://gethabit.dev/skills/anthropics/claude-md-improver
---

# CLAUDE.md Improver skill

The CLAUDE.md Improver skill audits the CLAUDE.md files in a repository, scores them against a quality rubric and proposes small targeted updates for teams that use Claude Code.

- Install the skill: `npx skills add anthropics/claude-plugins-official --skill claude-md-improver`
- Source: https://github.com/anthropics/claude-plugins-official/tree/HEAD/plugins/claude-md-management/skills/claude-md-improver
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your CLAUDE.md feels outdated; You set up a monorepo with many CLAUDE.md files; Build or test commands changed.
Skip it when: You do not use Claude Code; You want a CLAUDE.md written from scratch.

# Make it a habit: Keep every CLAUDE.md current.

Once a week your agent finds every CLAUDE.md in the repo, scores each one with the claude md improver rubric and writes a quality report. You approve the proposed diffs before any file changes. A score log keeps each file's grade for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly on Monday (schedule; Claude Code routine or cron; `0 9 * * 1`)
- **Verification:** report first, you approve. Hard checks: quality report lists every CLAUDE.md found; every file has a score out of 100; no CLAUDE.md changes before approval; each change comes with a diff and a reason. On fail: notify, max 0 retries.
- **Memory:** CLAUDE.md score log at `loops/claude-md-audit-loop/scores.md`. Read first: last score and open issues for each CLAUDE.md.

## Steps

1. **Discover files.** The agent finds every CLAUDE.md, .claude.md and .claude.local.md file in the repository.
2. **Assess quality.** It scores each file on commands, architecture, patterns, conciseness, currency and actionability.
3. **Write report.** It outputs the quality report with grades A to F before it changes anything.
4. **Propose diffs.** It shows small targeted additions as diffs, each with a short reason.
5. **Ask you.** You confirm which updates to apply.
6. **Apply updates.** It applies the approved changes with the Edit tool and keeps the existing structure.
7. **Log scores.** The loop writes each file's new score to the score log.

Stop rule: Stops after one audit of up to 50 CLAUDE.md files per run.

## Permissions

- Writes: **/CLAUDE.md, **/.claude.local.md, loops/claude-md-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/claude-md-audit-loop/scores.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly on Monday. Verification: report first, you approve. Memory: loops/claude-md-audit-loop/scores.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
