---
name: improve-ui
title: Improve UI skill
repo: ibelick/ui-skills
license: MIT
url: https://gethabit.dev/skills/ibelick/improve-ui
---

# Improve UI skill

The improve ui skill audits one product surface against its own design evidence, keeps only proven UI problems, and writes self-contained plans for another agent, for teams fighting design-system drift.

- Install the skill: `npx skills add ibelick/ui-skills --skill improve-ui`
- Source: https://github.com/ibelick/ui-skills/tree/HEAD/skills/improve-ui
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: reviewing an interface for drift; preparing a design handoff; cleaning up UI without a redesign.
Skip it when: building a new design from scratch; fixing broken product behavior.

# Make it a habit: Proven UI fixes, planned for handoff.

Runs every two weeks on one product surface. Your agent traces the rendered path, checks it against the surface's own design sources, keeps only findings with contract, runtime and correction proof, and asks you which to plan.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** biweekly surface audit (schedule; Claude Code routine; `0 10 1,15 * *`)
- **Verification:** proof gate, your pick. Hard checks: no product source files changed; every finding row has all columns including Confidence; at most three findings reported; plans exist only under design-plans/. On fail: stop, max 0 retries.
- **Memory:** design plans folder at `design-plans/`. Read first: existing plans to reconcile instead of duplicating.

## Steps

1. **Select the surface.** Pick one coherent surface and trace its routes, layouts and components.
2. **Rebuild the system.** Find current design sources such as DESIGN.md and record the design language.
3. **Prove findings.** Keep a candidate only with contract, runtime and correction proof.
4. **Vet findings.** Reopen every source and delete candidates that fail, overlap or invent intent.
5. **Report.** Show up to three findings and one improve-first pick.
6. **Ask you.** Ask which findings should become plans.
7. **Write plans.** Write one self-contained plan per chosen change under design-plans/.

Stop rule: Stops after one surface and three findings per run.

## Permissions

- Writes: design-plans/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`design-plans/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: biweekly surface audit. Verification: proof gate, your pick. Memory: design-plans/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
