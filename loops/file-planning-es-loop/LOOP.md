---
name: planning-with-files-es
title: Planning with Files (Spanish) skill
repo: othmanadi/planning-with-files
license: MIT
url: https://gethabit.dev/skills/othmanadi/planning-with-files-es
---

# Planning with Files (Spanish) skill

Planning with files (Spanish) keeps a task plan, findings and progress log on disk in Spanish, with hooks that re-read the plan so long agent tasks stay on track across context resets. For Spanish-speaking users running multi-step work.

- Install the skill: `npx skills add othmanadi/planning-with-files --skill planning-with-files-es`
- Source: https://github.com/othmanadi/planning-with-files/tree/HEAD/skills/i18n/planning-with-files-es
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: research with many tool calls; building a project in phases; resuming work after an interruption.
Skip it when: a simple question; editing one file.

# Make it a habit: Long tasks survive context resets.

For any task with many tool calls, your agent keeps task_plan.md, findings.md and progress.md on disk in Spanish. Hooks re-read the plan before each tool call, errors get logged, and check-complete.sh tells when all phases are done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** multi-step task starts (event; Claude Code hooks; `UserPromptSubmit hook on a task needing 5 or more tool calls`)
- **Verification:** all phases complete. Hard checks: task_plan.md exists before work starts; check-complete.sh reports every phase complete; every error is logged in the plan. On fail: retry, max 2 retries.
- **Memory:** plan, findings, progress at `task_plan.md`. Read first: current phase in task_plan.md, then findings.md and progress.md.

## Steps

1. **Restore state.** Resolve the plan folder with resolve-plan-dir.sh, read the three files and run git diff --stat.
2. **Create the plan.** Run init-session.sh for a new task and create only missing planning files.
3. **Save findings.** After every two search or browser steps, write key findings to findings.md.
4. **Re-read before deciding.** Read the plan before big decisions so the goal stays in view.
5. **Update after phases.** Mark phases complete and log errors and changed files.
6. **Check completion.** Run check-complete.sh and add new phases if more work is asked.

Stop rule: Stops when all phases are complete, or after three failed attempts on one error, then asks you.

## Permissions

- Writes: task_plan.md, findings.md, progress.md, .planning/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`task_plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: multi-step task starts. Verification: all phases complete. Memory: task_plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
