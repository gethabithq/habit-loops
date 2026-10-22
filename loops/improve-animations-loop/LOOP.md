---
name: improve-animations
title: Improve Animations skill
repo: emilkowalski/skills
license: MIT
url: https://gethabit.dev/skills/emilkowalski/improve-animations
---

# Improve Animations skill

The improve animations skill has your agent audit a codebase's motion code and write prioritized, self-contained fix plans that any agent can run. Read-only on source code. For teams who want an animation roadmap.

- Install the skill: `npx skills add emilkowalski/skills --skill improve-animations`
- Source: https://github.com/emilkowalski/skills/tree/HEAD/skills/improve-animations
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: the whole app feels sluggish; you want a roadmap of motion fixes; you hand fixes to cheaper agents.
Skip it when: you review one diff only; you want the fixes applied right now.

# Make it a habit: Ranked motion fixes, ready to execute.

Each month your agent maps the motion in your codebase, audits it across eight categories, vets every finding at its file:line, and writes self-contained plans into plans/. The reconcile pass marks done plans and refreshes stale references. Source code is never changed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly motion audit (schedule; Claude Code routine or cron; `0 9 1 * *`)
- **Verification:** read-only, you pick plans. Hard checks: git diff shows no changes outside plans/; every finding cites a file:line; each plan is stamped with git rev-parse --short HEAD; plans/README.md lists order and status. On fail: stop, max 0 retries.
- **Memory:** plans README board at `plans/README.md`. Read first: plan status, order and dependencies from the last audit.

## Steps

1. **Reconcile old plans.** Run the reconcile variant to mark done plans DONE and refresh stale file:line references.
2. **Recon the motion.** Map the stack, motion libraries, easing and duration tokens, personality and frequency of each animated element.
3. **Audit eight categories.** Audit against AUDIT.md, using read-only subagents for larger repos.
4. **Vet the findings.** Re-read each cited line and drop by-design, duplicate or exempt findings.
5. **Wait for your pick.** Show one table ranked by leverage and wait for you to choose, or take the top 3 to 5 when unattended.
6. **Write plans.** Write one plan per pick in plans/ with PLAN-TEMPLATE.md, exact values and a feel-check, then update plans/README.md.

Stop rule: Stops after one audit and at most five plans per run.

## Permissions

- Writes: plans/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`plans/README.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly motion audit. Verification: read-only, you pick plans. Memory: plans/README.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
