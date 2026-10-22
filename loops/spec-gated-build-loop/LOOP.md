---
name: develop
title: Develop skill
repo: jsmastery-pro/skills
license: MIT
url: https://gethabit.dev/skills/jsmastery-pro/develop
---

# Develop skill

Develop builds a feature, UI or backend, from an approved spec: it gates on undecided choices and routes them to architect, then reads the spec and AGENTS.md, builds, and advances the scope. For engineers using a spec-driven workflow.

- Install the skill: `npx skills add jsmastery-pro/skills --skill develop`
- Source: https://github.com/jsmastery-pro/skills/tree/HEAD/skills/develop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build from an approved spec; You add a page, API or service; You continue a scoped feature.
Skip it when: The design is still undecided; You are only fixing a bug.

# Make it a habit: Features built only from settled specs.

When a scope item is ready to build, your agent runs the develop skill: it applies the input coverage test, stops and routes to architect if a value has no named source, then reads the spec and AGENTS.md, builds the UI or logic, and advances the scope.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start a build (manual; Claude Code routine; `/develop <task>`)
- **Verification:** spec gate + build. Hard checks: every required value has a named source or the build stopped at the gate; the project builds or the dev server runs; the scope feature status and code pointer are updated. On fail: stop, max 0 retries.
- **Memory:** feature scope file at `docs/scope/scope.md`. Read first: this feature's scope section and its governing spec pointer.

## Steps

1. **Run the spec gate.** Enumerate every value the build must produce and check the spec names a source for each.
2. **Route if owed.** If a source is unnamed, stop and route to architect or record an Assumed spec.
3. **Classify the track.** Decide whether the work is UI, logical or both from the spec.
4. **Read conventions.** Read the governing spec, the nearest AGENTS.md and the matching build guide.
5. **Build.** Follow flow/build.md to build, asking only what the design left open.
6. **Advance the scope.** Update the feature status, milestone boxes and code pointer in the scope file.

Stop rule: Stops at the gate when a decision is owed, or after one feature slice is built.

## Permissions

- Writes: src/**, docs/scope/**, docs/specs/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/scope/scope.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start a build. Verification: spec gate + build. Memory: docs/scope/scope.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
