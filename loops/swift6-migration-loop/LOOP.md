---
name: swift-concurrency
title: Swift Concurrency skill
repo: AvdLee/Swift-Concurrency-Agent-Skill
license: MIT
url: https://gethabit.dev/skills/avdlee/swift-concurrency
---

# Swift Concurrency skill

The swift concurrency skill helps Swift developers diagnose concurrency errors, move callback code to async/await and migrate to Swift 6 with actors, @MainActor, Sendable and task isolation.

- Install the skill: `npx skills add AvdLee/Swift-Concurrency-Agent-Skill --skill swift-concurrency`
- Source: https://github.com/AvdLee/Swift-Concurrency-Agent-Skill/tree/HEAD/skills/swift-concurrency
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Fixing Sendable or actor isolation errors; Migrating a project to Swift 6; Converting callbacks to async/await.
Skip it when: Projects not written in Swift; Code with no concurrency.

# Make it a habit: One diagnostic category cleared per run.

Each night the agent reads the project's concurrency settings, builds, fixes one category of concurrency diagnostics with the smallest safe change, rebuilds and runs the tests. A board tracks the confirmed settings and the categories left.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every weeknight (schedule; Claude Code routine; `0 2 * * 1-5`)
- **Verification:** build, tests + settings. Hard checks: swift build passes with no new diagnostics; swift test passes; every @unchecked Sendable or nonisolated(unsafe) has a documented safety invariant; one change fixes only one diagnostic category. On fail: stop, max 1 retries.
- **Memory:** migration board at `loops/swift6-migration-loop/board.md`. Read first: confirmed build settings and remaining diagnostic categories per module.

## Steps

1. **Read settings.** The agent reads Package.swift or .pbxproj for language mode, strict concurrency and default isolation.
2. **Confirm unknowns.** If a setting is unknown, it asks the developer before any migration fix.
3. **Build.** It runs swift build to surface diagnostics.
4. **Fix one category.** It fixes one category, such as all Sendable issues, with the smallest safe change.
5. **Rebuild and test.** It rebuilds clean, then runs swift test.
6. **Update the board.** It marks the category done and names the next one.

Stop rule: Stops after one diagnostic category in one module per run.

## Permissions

- Writes: loops/swift6-migration-loop/**, Package.swift
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/swift6-migration-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every weeknight. Verification: build, tests + settings. Memory: loops/swift6-migration-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
