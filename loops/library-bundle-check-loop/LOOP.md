---
name: tsdown
title: tsdown skill
repo: rolldown/tsdown
license: MIT
url: https://gethabit.dev/skills/rolldown/tsdown
---

# tsdown skill

Tsdown is a skill for library authors that bundles TypeScript and JavaScript libraries with tsdown and Rolldown: declarations, ESM and CJS formats, dependency handling, package validation and migration from tsup.

- Install the skill: `npx skills add rolldown/tsdown --skill tsdown`
- Source: https://github.com/rolldown/tsdown/tree/HEAD/skills/tsdown
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build an npm library; You need .d.ts files; You migrate from tsup.
Skip it when: You bundle a web app; You build with Node below 22.18.

# Make it a habit: Library builds valid before publish.

On every pull request to a TypeScript library, your agent runs tsdown with the project config, generating declarations, and validates the package with publint and attw. A log keeps build warnings and package issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions; `pull_request.opened`)
- **Verification:** build and package checks. Hard checks: npx tsdown builds with no errors; type declarations are emitted when dts is true; publint and attw pass; tests pass on the built output. On fail: notify, max 1 retries.
- **Memory:** build warnings log at `loops/library-bundle-check-loop/run-log.md`. Read first: recent warnings and package issues.

## Steps

1. **Check Node.** Build on Node.js 22.18.0 or higher.
2. **Build.** Run npx tsdown --config tsdown.config.ts.
3. **Validate package.** Use publint and attw, set to ci-only in the config.
4. **Test the output.** Run the tests on the built output for each supported Node version.
5. **Log.** Write warnings and package issues into the run log.

Stop rule: Stops after one build per pull request, with one retry.

## Permissions

- Writes: dist/**, loops/library-bundle-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/library-bundle-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: build and package checks. Memory: loops/library-bundle-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
