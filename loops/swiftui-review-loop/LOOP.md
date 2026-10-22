---
name: swiftui-expert-skill
title: SwiftUI Expert Skill skill
repo: AvdLee/SwiftUI-Agent-Skill
license: MIT
url: https://gethabit.dev/skills/avdlee/swiftui-expert-skill
---

# SwiftUI Expert Skill skill

The swiftui expert skill helps agents write and review SwiftUI for iOS and macOS: state and data flow, layout, lists, animation, deprecated APIs and Instruments trace analysis. For Apple developers who want correct, fast SwiftUI.

- Install the skill: `npx skills add AvdLee/SwiftUI-Agent-Skill --skill swiftui-expert-skill`
- Source: https://github.com/AvdLee/SwiftUI-Agent-Skill/tree/HEAD/skills/swiftui-expert-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review or refactor SwiftUI code; You migrate deprecated SwiftUI APIs; You analyze an Instruments trace.
Skip it when: The app is UIKit only; You need server-side Swift.

# Make it a habit: SwiftUI changes pass the checklist.

On each pull request with SwiftUI code, your agent runs swiftui expert skill in review mode: it routes each topic to its reference, flags deprecated APIs from latest-apis.md and checks the correctness checklist. Findings go to a log for the next review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes Swift files (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.swift`)
- **Verification:** checklist passes. Hard checks: every @State and @FocusState property is private; no ForEach uses .indices or \.offset; every .animation call has a value parameter. On fail: notify, max 0 retries.
- **Memory:** review findings log at `loops/swiftui-review-loop/findings.md`. Read first: soft-deprecated APIs flagged before and open findings.

## Steps

1. **Read the change.** Read the Swift files and pick the topics that apply.
2. **Route topics.** Open the matching reference from the topic router for each one.
3. **Check APIs.** Compare against latest-apis.md, replace hard-deprecated APIs and flag soft-deprecated ones.
4. **Check gating.** Make sure version-specific APIs use #available with fallbacks.
5. **Run the checklist.** Walk the correctness checklist for state, ForEach, environment and animation.
6. **Report.** List findings and give performance ideas as suggestions only.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/swiftui-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/swiftui-review-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes Swift files. Verification: checklist passes. Memory: loops/swiftui-review-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
