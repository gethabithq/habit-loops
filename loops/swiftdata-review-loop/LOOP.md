---
name: swiftdata-pro
title: SwiftData Pro skill
repo: twostraws/swiftdata-agent-skill
license: MIT
url: https://gethabit.dev/skills/twostraws/swiftdata-pro
---

# SwiftData Pro skill

The swiftdata pro skill writes and reviews SwiftData code with modern APIs: relationships, delete rules, safe predicates, CloudKit limits and indexing. For iOS developers who build apps on SwiftData.

- Install the skill: `npx skills add twostraws/swiftdata-agent-skill --skill swiftdata-pro`
- Source: https://github.com/twostraws/swiftdata-agent-skill/tree/HEAD/swiftdata-pro
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review SwiftData models; Predicates crash at runtime; You sync data with CloudKit.
Skip it when: The app uses Core Data only; There is no Swift code.

# Make it a habit: SwiftData bugs caught before merge.

When a pull request changes Swift model or query code, your agent reviews it with swiftdata-pro: core rules, predicate safety, and CloudKit, indexing or inheritance checks when they apply. Findings are listed by file with a fix, and a log keeps rules that keep coming back.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Swift pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened with changed .swift files`)
- **Verification:** build plus rule review. Hard checks: project builds; tests pass; every finding names a file, a line and a rule. On fail: notify, max 0 retries.
- **Memory:** repeated rule log at `loops/swiftdata-review-loop/runs.md`. Read first: rules this project broke in earlier reviews.

## Steps

1. **Core rules.** The agent checks the changed code against references/core-rules.md.
2. **Predicates.** It checks predicates for unsafe or unsupported patterns with references/predicates.md.
3. **Platform checks.** It loads references/cloudkit.md, references/indexing.md or references/class-inheritance.md only when the project needs them.
4. **Report by file.** It lists each real issue with file, line, rule and a short before and after fix.
5. **Prioritise.** It ends with the most important changes first.
6. **Log.** It adds the broken rules to the log for the next review.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/swiftdata-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/swiftdata-review-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Swift pull request opened. Verification: build plus rule review. Memory: loops/swiftdata-review-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
