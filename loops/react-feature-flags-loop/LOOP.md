---
name: feature-flags
title: React feature flags skill
repo: react/react
license: MIT
url: https://gethabit.dev/skills/react/feature-flags
---

# React feature flags skill

The react feature flags skill explains React's flag files, @gate pragmas, inline gate() checks and __VARIANT__ flags, and how to debug channel-specific test failures. For contributors to React core.

- Install the skill: `npx skills add react/react --skill feature-flags`
- Source: https://github.com/react/react/tree/HEAD/.claude/skills/feature-flags
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A feature flag test fails; You add a new React flag; A test fails on one channel only.
Skip it when: You use flags in your own app; Your change touches no flags.

# Make it a habit: Flags consistent across every fork.

When a pull request changes React feature flags, your agent checks that each flag is in ReactFeatureFlags.js and every fork file, that gates use the right syntax, and that both www variants pass. A log keeps flags with open issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** flag files change (event; GitHub Actions or Claude Code routine; `pull_request paths: packages/shared/ReactFeatureFlags.js, packages/shared/forks/ReactFeatureFlags.*.js`)
- **Verification:** forks match, variants pass. Hard checks: every new flag exists in all fork files; gates use gate(flags => flags.name), not gate('name'); /test www and /test www variant false both pass. On fail: notify, max 0 retries.
- **Memory:** flag issues log at `loops/react-feature-flags-loop/log.md`. Read first: flags that were missing from forks or failed a variant.

## Steps

1. **List changed flags.** The agent reads which flags the pull request adds or changes.
2. **Check fork files.** It confirms each flag is set in the www, native-fb and test-renderer forks too.
3. **Compare channels.** It runs /flags --diff between channels to see the values.
4. **Check gates.** It checks that @gate is used only when a feature is fully missing, and inline gate() otherwise.
5. **Test both variants.** For __VARIANT__ flags it runs /test www and /test www variant false.
6. **Log the result.** It writes missing forks and failing variants to the log and notifies you.

Stop rule: Stops after one pull request per run, checking at most ten flags.

## Permissions

- Writes: loops/react-feature-flags-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-feature-flags-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: flag files change. Verification: forks match, variants pass. Memory: loops/react-feature-flags-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
