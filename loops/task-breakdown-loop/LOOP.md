---
name: planning-and-task-breakdown
title: Planning and Task Breakdown skill
repo: addyosmani/agent-skills
license: MIT
url: https://gethabit.dev/skills/addyosmani/planning-and-task-breakdown
---

# Planning and Task Breakdown skill

The planning and task breakdown skill by Addy Osmani turns a spec into small, ordered, verifiable tasks with acceptance criteria, dependencies and checkpoints. For developers and agents who need a clear build order before coding.

- Install the skill: `npx skills add addyosmani/agent-skills --skill planning-and-task-breakdown`
- Source: https://github.com/addyosmani/agent-skills/tree/HEAD/skills/planning-and-task-breakdown
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You have a spec and need tasks; A task feels too large to start; Work will run across several agents or sessions.
Skip it when: The change is one file with obvious scope; The spec already holds well-defined tasks.

# Make it a habit: Turn each spec into small tasks.

When a spec is approved, your agent reads it in plan mode, maps dependencies, slices the work vertically and writes tasks/plan.md and tasks/todo.md with checkpoints. Hard checks catch tasks without criteria, and you approve the plan.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** spec gets approved (event; Claude Code routine or GitHub Actions; `spec file merged or marked approved`)
- **Verification:** task check + your approval. Hard checks: every task has acceptance criteria; every task has a verification step; no task touches more than about five files; a checkpoint follows every two to three tasks; no unfinished tasks/plan.md or tasks/todo.md was overwritten. On fail: notify, max 1 retries.
- **Memory:** plan and todo files at `tasks/plan.md`. Read first: open tasks in tasks/plan.md and tasks/todo.md.

## Steps

1. **Plan mode.** Read the spec and code without writing any code, and note risks and unknowns.
2. **Map dependencies.** Draw what depends on what so foundations come first.
3. **Slice vertically.** Cut the work into complete feature paths instead of layers.
4. **Write tasks.** Give each task a description, acceptance criteria, verification, dependencies, likely files and a size.
5. **Order and checkpoint.** Put risky tasks early and add a checkpoint after every two or three tasks.
6. **Check old plans.** If tasks/plan.md still has unchecked tasks for other work, stop and ask you.
7. **Get approval.** Save the files or tracker items and ask you to review the plan.

Stop rule: Stops after one spec per run and one retry of the checks.

## Permissions

- Writes: tasks/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`tasks/plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: spec gets approved. Verification: task check + your approval. Memory: tasks/plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
