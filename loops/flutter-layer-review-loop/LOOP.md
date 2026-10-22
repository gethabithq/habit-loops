---
name: flutter-architecture
title: Flutter Architecture skill
repo: madteacher/mad-agents-skills
license: MIT
url: https://gethabit.dev/skills/madteacher/flutter-architecture
---

# Flutter Architecture skill

Flutter architecture is a skill for Flutter developers who design, review or refactor app structure with MVVM, layered boundaries, feature-first or layer-first layout, repositories, services and Command and Result patterns.

- Install the skill: `npx skills add madteacher/mad-agents-skills --skill flutter-architecture`
- Source: https://github.com/madteacher/mad-agents-skills/tree/HEAD/flutter-architecture
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add a Flutter feature; You fix cross-feature imports; You pick a Flutter structure.
Skip it when: You build a tiny prototype; You do not use Flutter.

# Make it a habit: Flutter features keep clean layer boundaries.

On each pull request to a Flutter app, your agent checks layer and feature boundaries: no cross-feature imports, ViewModels without direct I/O, repositories independent of UI. It runs flutter analyze and focused tests and logs violations.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes lib/ (event; GitHub Actions or Claude Code routine; `pull_request.opened touching lib/`)
- **Verification:** analyze and tests pass. Hard checks: flutter analyze passes; focused flutter test suites pass; no feature imports another feature's implementation files. On fail: notify, max 1 retries.
- **Memory:** layer violations log at `loops/flutter-layer-review-loop/run-log.md`. Read first: violations found before and the chosen structure.

## Steps

1. **Read the project.** Inspect pubspec.yaml, lib/ and existing state, routing and DI conventions.
2. **Check imports.** Confirm new imports respect the feature-first or layer-first boundary.
3. **Check ViewModels.** Confirm ViewModels hold UI state and do no platform, file or network I/O.
4. **Check data layer.** Confirm repositories stay UI-independent and services stay stateless.
5. **Validate.** Run flutter analyze and focused flutter test suites.
6. **Report.** Log layer violations, missing tests and residual risks.

Stop rule: Stops after one pull request per run, with one retry.

## Permissions

- Writes: loops/flutter-layer-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flutter-layer-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes lib/. Verification: analyze and tests pass. Memory: loops/flutter-layer-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
