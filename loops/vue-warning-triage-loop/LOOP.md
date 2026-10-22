---
name: vue-debug-guides
title: Vue Debug Guides skill
repo: vuejs-ai/skills
license: MIT
url: https://gethabit.dev/skills/vuejs-ai/vue-debug-guides
---

# Vue Debug Guides skill

The vue debug guides skill gives Vue 3 developers an index of symptoms with matching fixes for runtime errors, warnings, async failures and SSR hydration bugs.

- Install the skill: `npx skills add vuejs-ai/skills --skill vue-debug-guides`
- Source: https://github.com/vuejs-ai/skills/tree/HEAD/skills/vue-debug-guides
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A Vue 3 app shows a runtime warning; SSR and client renders differ; Reactivity stops updating.
Skip it when: The app uses Vue 2 only; You want general best practices.

# Make it a habit: Vue warnings get fixed, not ignored.

When CI or a dev run logs a Vue runtime error, warning or hydration mismatch, your agent matches it to the right vue-debug-guides reference, applies the fix, runs the tests and logs which guide solved which symptom.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Vue warning in logs (event; GitHub Actions or Claude Code routine; `CI log contains [Vue warn] or a hydration mismatch`)
- **Verification:** warning gone, tests pass. Hard checks: the same warning no longer appears in the rerun log; tests pass; build passes. On fail: retry, max 2 retries.
- **Memory:** symptom to guide log at `loops/vue-warning-triage-loop/run-log.md`. Read first: symptoms seen before and the guide that fixed them.

## Steps

1. **Read the log.** The agent checks if this symptom was fixed before and which guide helped.
2. **Collect warnings.** It gathers the Vue errors and warnings from the latest run.
3. **Match a guide.** It finds the symptom in the skill's index, such as reactivity, watchers, templates or SSR, and opens that reference file.
4. **Apply the fix.** It changes the code the way the reference describes.
5. **Rerun and test.** It reruns the build and tests and checks the warning is gone.
6. **Record.** It writes the symptom, guide and result to the run log.

Stop rule: Stops after fixing at most five warnings per run, with up to two retries each.

## Permissions

- Writes: src/**, loops/vue-warning-triage-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/vue-warning-triage-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Vue warning in logs. Verification: warning gone, tests pass. Memory: loops/vue-warning-triage-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
