---
name: scope
title: Scope skill
repo: jsmastery-pro/skills
license: MIT
url: https://gethabit.dev/skills/jsmastery-pro/scope
---

# Scope skill

Scope turns a product idea into a living, coarse plan in docs/scope/ and keeps it current: plan a product or next slice, enroll a feature, or reconcile after shipping and queue what is next. For teams running a spec-driven build workflow.

- Install the skill: `npx skills add jsmastery-pro/skills --skill scope`
- Source: https://github.com/jsmastery-pro/skills/tree/HEAD/skills/scope
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You plan a new product; You queue the next slice; You reconcile the plan after shipping.
Skip it when: You want to design one feature; You want to write build tasks.

# Make it a habit: The scope stays honest after shipping.

After each shipped slice, your agent runs /scope with no argument to reconcile what shipped, surface plan versus reality drift, enroll features found during the build and queue the next slice. It writes only coarse scope rows in docs/scope/, never specs or code.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** a slice ships (event; Claude Code routine; `after a feature merges`)
- **Verification:** scope matches reality. Hard checks: every feature row has a status; code or specs with no scope row are surfaced as drift; no tool, library or provider is named in the scope. On fail: notify, max 0 retries.
- **Memory:** scope file at `docs/scope/scope.md`. Read first: the At a glance table, feature statuses and in-progress resume points.

## Steps

1. **Read where things stand.** Open with git branch, ahead/behind, feature counts by status and each in-progress resume point.
2. **Reconcile shipped work.** Update feature statuses to match what actually shipped.
3. **Surface drift.** Flag code or specs that have no scope row.
4. **Enroll new features.** Add coarse rows for needs surfaced during the build, with intent, order and tier.
5. **Queue the next slice.** Reorder and mark which features need a spec first.
6. **Stay tool-agnostic.** Mark any feature implying a tool choice as needs a decision, never naming the tool.

Stop rule: Stops after one reconcile pass per run.

## Permissions

- Writes: docs/scope/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/scope/scope.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: a slice ships. Verification: scope matches reality. Memory: docs/scope/scope.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
