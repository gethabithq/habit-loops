---
name: brief-to-tasks
title: Brief to Tasks skill
repo: julianoczkowski/designer-skills
license: Apache-2.0
url: https://gethabit.dev/skills/julianoczkowski/brief-to-tasks
---

# Brief to Tasks skill

The brief to tasks skill breaks a design brief into an ordered checklist of independently buildable vertical slices, based on the existing codebase, and saves it as TASKS.md next to the brief. For designers and developers planning a UI build.

- Install the skill: `npx skills add julianoczkowski/designer-skills --skill brief-to-tasks`
- Source: https://github.com/julianoczkowski/designer-skills/tree/HEAD/brief-to-tasks
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You have a finished design brief; You need a build order; You want tasks that reuse existing components.
Skip it when: You have no brief or clear idea yet; The work is a single tiny fix.

# Make it a habit: Turn design briefs into buildable tasks.

When a design brief is ready, your agent reads it with any architecture and token files, scans existing components, pages and dependencies, splits the work into vertical slices ordered by dependency, visibility and risk, and saves TASKS.md next to the brief.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** a brief is written (event; Claude Code routine; `a new or changed .design/*/DESIGN_BRIEF.md`)
- **Verification:** task list saved, valid. Hard checks: TASKS.md exists in the brief's .design/<feature-slug>/ folder; every task says it reuses, modifies or creates components; no task is only project setup; the list ends with a design review task. On fail: retry, max 1 retries.
- **Memory:** TASKS.md checklist at `.design/<feature-slug>/TASKS.md`. Read first: the brief and existing task checklist.

## Steps

1. **Read the brief.** Your agent reads the newest DESIGN_BRIEF.md, plus INFORMATION_ARCHITECTURE.md and tokens if present.
2. **Scan the codebase.** It lists components, pages, theme files, naming rules, tests and dependencies.
3. **Classify components.** It marks each as reused, modified or new.
4. **Slice the work.** It writes tasks that each cover structure, styling and interaction.
5. **Order tasks.** It puts dependencies, the most visible element and the riskiest piece first.
6. **Save.** It writes TASKS.md from the template, ending with a /design-review task.

Stop rule: Stops after one brief and one revision.

## Permissions

- Writes: .design/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.design/<feature-slug>/TASKS.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: a brief is written. Verification: task list saved, valid. Memory: .design/<feature-slug>/TASKS.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
