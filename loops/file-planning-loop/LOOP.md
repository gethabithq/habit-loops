---
name: planning-with-files-zh
title: Planning with Files (Chinese) skill
repo: OthmanAdi/planning-with-files
license: MIT
url: https://gethabit.dev/skills/othmanadi/planning-with-files-zh
---

# Planning with Files (Chinese) skill

The Planning with Files (Chinese) skill is the Chinese version of a file-based planning system for multi-step agent work: it keeps task_plan.md, findings.md and progress.md on disk and rereads them through hooks. For agents on long research or build tasks.

- Install the skill: `npx skills add OthmanAdi/planning-with-files --skill planning-with-files-zh`
- Source: https://github.com/OthmanAdi/planning-with-files/tree/HEAD/skills/i18n/planning-with-files-zh
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A task needs more than 5 tool calls; You run research across many sources; You resume work after an interruption.
Skip it when: You ask a simple question; You edit a single file.

# Make it a habit: Long tasks keep plans on disk.

When a multi-step task starts, your agent restores or creates task_plan.md, findings.md and progress.md, rereads the plan before each decision, logs every error, and checks with check-complete.sh that all phases are done before it stops.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** multi-step task starts (event; Claude Code; `UserPromptSubmit hook for tasks with 5+ tool calls`)
- **Verification:** phases complete, else ask. Hard checks: task_plan.md exists before work starts; scripts/check-complete.sh reports all phases complete; every error is logged in the plan file. On fail: notify, max 2 retries.
- **Memory:** plan, findings, progress at `task_plan.md`. Read first: current phase in task_plan.md, then findings.md and progress.md.

## Steps

1. **Restore state.** The agent resolves the plan directory with scripts/resolve-plan-dir.sh, reads the three files and runs git diff --stat.
2. **Create the plan.** For a new task it runs scripts/init-session.sh and creates only the missing files from the templates.
3. **Save findings.** After every 2 view or search actions it writes key findings to findings.md, never web content to task_plan.md.
4. **Reread before deciding.** Before a big decision it reads the plan again to keep the goal in view.
5. **Update after each phase.** It marks the phase complete, logs errors and notes changed files.
6. **Three-failure rule.** It changes approach after each failure and asks you for guidance after 3 failed attempts.
7. **Check completion.** It runs scripts/check-complete.sh before it ends the session.

Stop rule: Stops when all phases are complete, or after 3 failed attempts on one step it stops and asks you.

## Permissions

- Writes: task_plan.md, findings.md, progress.md, .planning/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`task_plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: multi-step task starts. Verification: phases complete, else ask. Memory: task_plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
