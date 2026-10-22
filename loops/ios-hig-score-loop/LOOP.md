---
name: ios-hig-design
title: iOS HIG design skill
repo: wondelai/skills
license: MIT
url: https://gethabit.dev/skills/wondelai/ios-hig-design
---

# iOS HIG design skill

The ios hig design skill helps designers and developers build native iPhone and iPad interfaces with safe areas, Dynamic Type, Dark Mode, SF Symbols, accessibility and a 10-point score.

- Install the skill: `npx skills add wondelai/skills --skill ios-hig-design`
- Source: https://github.com/wondelai/skills/tree/HEAD/ios-hig-design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: building a SwiftUI screen; checking HIG compliance; making an app feel native.
Skip it when: Android app design; general web UI polish.

# Make it a habit: Every screen scores toward 10/10.

Runs on each pull request that changes iOS screens. Your agent scores the screen with the skill's six-row quick diagnostic plus native idiom points, lists fixes to reach 10/10, and keeps scores per screen.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** iOS screen changed (event; GitHub Actions or Claude Code routine; `pull request touches SwiftUI or UIKit views`)
- **Verification:** HIG score per screen. Hard checks: all touch targets at least 44 x 44pt; no hardcoded font sizes; every interactive element has an accessibilityLabel. Critic: claude-opus-5-5, pass at 9/10. On fail: notify, max 1 retries.
- **Memory:** screen score history at `loops/ios-hig-score-loop/scores.md`. Read first: last score and open fixes for each screen.

## Steps

1. **Find changed screens.** List the iOS views touched by the change.
2. **Run diagnostic.** Check safe areas, touch targets, Dark Mode, Dynamic Type, VoiceOver and native navigation.
3. **Score idiom.** Add points for semantic colors, system controls, standard gestures and SF Symbols.
4. **List fixes.** State the score and the exact changes needed to reach 10/10.
5. **Update history.** Save the new score next to the previous one for each screen.

Stop rule: Stops after scoring 5 screens per run.

## Permissions

- Writes: loops/ios-hig-score-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ios-hig-score-loop/scores.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: iOS screen changed. Verification: HIG score per screen. Memory: loops/ios-hig-score-loop/scores.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
