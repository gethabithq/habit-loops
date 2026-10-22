---
name: flutter-animations
title: Flutter Animations skill
repo: MADTeacher/mad-agents-skills
license: MIT
url: https://gethabit.dev/skills/madteacher/flutter-animations
---

# Flutter Animations skill

The flutter animations skill helps Flutter developers add, fix, refactor and debug motion: implicit and explicit animations, Hero transitions, staggered timing, physics, curves and reduced-motion support.

- Install the skill: `npx skills add MADTeacher/mad-agents-skills --skill flutter-animations`
- Source: https://github.com/MADTeacher/mad-agents-skills/tree/HEAD/flutter-animations
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add or fix a Flutter animation; An animation leaks or janks; You need Hero or staggered motion.
Skip it when: The app is not built with Flutter; The change has no motion at all.

# Make it a habit: Clean Flutter motion, analyzer approved.

When a pull request changes Flutter animation code, your agent picks the smallest animation model, fixes lifecycle and reduced-motion gaps, then runs dart format, flutter analyze and focused tests. It logs what stayed visually unverified.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request touches animations (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize on Dart files with animation code`)
- **Verification:** analyzer, format and tests. Hard checks: flutter analyze reports no issues; dart format leaves no diff; focused widget or integration tests pass; every AnimationController is disposed. On fail: retry, max 2 retries.
- **Memory:** animation run log at `loops/flutter-animation-check-loop/runs.md`. Read first: open items that were never checked visually.

## Steps

1. **Read the request.** Decide if the change adds, fixes, refactors, debugs or explains an animation.
2. **Inspect the context.** Look at the widget tree, state, navigation, theme, tests and existing animation code first.
3. **Pick the model.** Choose implicit, explicit, Hero, staggered or physics motion, whichever is smallest for the behavior.
4. **Implement in style.** Keep controllers in the owning state object, dispose them and keep rebuild regions small.
5. **Respect reduced motion.** Check MediaQuery.disableAnimations and give a static path for motion that is not essential.
6. **Validate.** Run dart format, flutter analyze and focused tests on the touched code.
7. **Log the gaps.** Write down what was checked statically and what still needs a visual look.

Stop rule: Stops after one pull request and at most two fix retries.

## Permissions

- Writes: lib/**, loops/flutter-animation-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flutter-animation-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request touches animations. Verification: analyzer, format and tests. Memory: loops/flutter-animation-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
