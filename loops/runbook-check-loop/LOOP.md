---
name: writing-runbooks
title: Writing Runbooks skill
repo: riekelt/technical-writer
license: MIT
url: https://gethabit.dev/skills/riekelt/writing-runbooks
---

# Writing Runbooks skill

The writing runbooks skill gives a runbook skeleton, a risk legend, symptom-first troubleshooting and migration-guide rules, for engineers writing procedures that someone will run under time pressure.

- Install the skill: `npx skills add riekelt/technical-writer --skill writing-runbooks`
- Source: https://github.com/riekelt/technical-writer/tree/HEAD/plugins/technical-writer/skills/writing-runbooks
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Writing a runbook or setup guide; Writing a migration or deprecation guide; Adding troubleshooting entries.
Skip it when: Design rationale; Reference material nobody executes.

# Make it a habit: Runbooks stay runnable and honest.

When a runbook or setup guide changes, the agent checks it against the runbook rules: a legend up front, numbered one-action steps, a rollback for every state change and a verify-it-worked section. Branches never run stay marked as draft.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** runbook pull request (event; GitHub Actions; `pull_request changes a runbook or guide`)
- **Verification:** runbook structure check. Hard checks: every state-changing step names a rollback or says none exists; a verify-it-worked section with a proving command exists; unknown values stay as visible bracketed placeholders; steps are numbered with one action each. On fail: notify, max 1 retries.
- **Memory:** untested branches board at `loops/runbook-check-loop/board.md`. Read first: branches still marked draft and waiting for a real run.

## Steps

1. **Load background.** The agent reads the technical-writing skill first.
2. **Check structure.** Scope in the title, a risk legend, a TL;DR happy path, then numbered steps.
3. **Check commands.** Each command must paste as-is with concrete example values.
4. **Check rollback.** Each state change names its undo, or says plainly it cannot be undone.
5. **Check the end.** The last section shows the end state and the command that proves it.
6. **Mark drafts.** Branches with no real run behind them are marked draft and added to the board.

Stop rule: Stops after one pull request and at most 3 runbooks per run.

## Permissions

- Writes: loops/runbook-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/runbook-check-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: runbook pull request. Verification: runbook structure check. Memory: loops/runbook-check-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
