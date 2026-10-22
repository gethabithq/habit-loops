---
name: planning-with-files-zht
title: Planning with Files (Traditional Chinese) skill
repo: othmanadi/planning-with-files
license: MIT
url: https://gethabit.dev/skills/othmanadi/planning-with-files-zht
---

# Planning with Files (Traditional Chinese) skill

Planning with Files (Traditional Chinese) makes an agent keep task_plan.md, findings.md and progress.md on disk so long tasks survive restarts, with hooks that reinject the plan. For people who run multi-step research or build work.

- Install the skill: `npx skills add othmanadi/planning-with-files --skill planning-with-files-zht`
- Source: https://github.com/othmanadi/planning-with-files/tree/HEAD/skills/i18n/planning-with-files-zht
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A task needs many tool calls; You run long research; You resume work after a break.
Skip it when: It is a simple question; You edit a single file.

# Make it a habit: Long tasks survive every restart.

For each multi-step task, your agent keeps task_plan.md, findings.md and progress.md on disk, rereads the plan before decisions, logs every error and updates progress after each phase. A check script confirms all phases are complete.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new multi-step task (manual; Claude Code session; `user starts a task needing more than 5 tool calls`)
- **Verification:** all phases complete. Hard checks: scripts/check-complete.sh reports every phase complete; task_plan.md exists before work starts; every error is listed in the plan. On fail: retry, max 2 retries.
- **Memory:** plan, findings, progress at `task_plan.md`. Read first: the current phase in task_plan.md, findings.md and progress.md.

## Steps

1. **Restore state.** The agent resolves the plan folder and reads task_plan.md, progress.md and findings.md.
2. **Check changes.** It runs git diff --stat to see changes not yet recorded.
3. **Init if new.** For a new task it runs scripts/init-session.sh to create the planning files.
4. **Save findings.** After every two view or search actions it writes key findings to findings.md.
5. **Update phases.** After each phase it marks the status, notes errors and lists changed files.
6. **Verify.** It runs scripts/check-complete.sh before calling the task done.

Stop rule: Stops after one task; after three failed attempts on the same error it asks the user.

## Permissions

- Writes: task_plan.md, findings.md, progress.md, .planning/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`task_plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new multi-step task. Verification: all phases complete. Memory: task_plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
