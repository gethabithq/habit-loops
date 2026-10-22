---
name: next-cache-components-optimizer
title: Next Cache Components Optimizer skill
repo: vercel/next.js
license: MIT
url: https://gethabit.dev/skills/vercel/next-cache-components-optimizer
---

# Next Cache Components Optimizer skill

The next cache components optimizer skill helps Next.js teams make routes paint instantly, using a failing instant() test that turns green and then guards against regressions.

- Install the skill: `npx skills add vercel/next.js --skill next-cache-components-optimizer`
- Source: https://github.com/vercel/next.js/tree/HEAD/skills/next-cache-components-optimizer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A route has a slow first paint; Client navigation is not instant; You want instant() regression tests.
Skip it when: You run Next.js older than 16.3; Cache Components is not adopted yet.

# Make it a habit: One more route paints instantly.

Per run your agent picks one Next.js route and entry point, writes a failing instant() test on a production build, applies the matching static shell fix until it passes, proves it with a revert differential and ships the test as a guard.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** route picked for optimizing (manual; Claude Code routine or GitHub Actions; `you name a route and entry point`)
- **Verification:** RED then GREEN, differential. Hard checks: the locked instant() test fails before the fix on a production build; the same test passes after the fix; reverting only the fix makes it fail again; the unlocked baseline test is deleted; the complete in-scope test command from the rig passes. On fail: retry, max 2 retries.
- **Memory:** instant-nav rig file at `instant-nav.rig.md`. Read first: build, test user and navigation contracts.

## Steps

1. **Check prereqs.** The agent confirms Next.js 16.3+ with cacheComponents: true and a matching @next/playwright.
2. **Read the rig.** It reads instant-nav.rig.md, or writes it on first use, and the Optimizing the static shell guide.
3. **Baseline.** Without the lock it confirms SHELL_MARKER renders for the test user.
4. **Write RED.** It wraps the navigation in instant() and confirms the RED is trustworthy before fixing.
5. **Fix.** It applies the guide pattern that matches the blocker until the locked test is GREEN.
6. **Parity.** It checks the route renders the same content, redirects and state as before.
7. **Differential.** It reverts only the fix to get RED, re-applies for GREEN, and runs the full rig command.
8. **Review.** It walks the PR checklist and removes the baseline test.

Stop rule: Stops after one route and entry point per run, with at most two fix retries.

## Permissions

- Writes: app/**, src/**, e2e/**, instant-nav.rig.md, next.config.ts
- Network: nextjs.org
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`instant-nav.rig.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: route picked for optimizing. Verification: RED then GREEN, differential. Memory: instant-nav.rig.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
