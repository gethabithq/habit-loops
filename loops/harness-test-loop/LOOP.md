---
name: test-harness
title: Test Harness skill
repo: zernie/vigiles
license: MIT
url: https://gethabit.dev/skills/zernie/test-harness
---

# Test Harness skill

The test harness skill helps Claude Code users test hooks, skills, agents, settings and CLAUDE.md with vigiles, picking unit, deterministic or eval tiers and keeping eval results honest in CI.

- Install the skill: `npx skills add zernie/vigiles --skill test-harness`
- Source: https://github.com/zernie/vigiles/tree/HEAD/skills/test-harness
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You check that a hook blocks what it should; You test that a skill triggers; You confirm injected context reaches the model.
Skip it when: You test application code; You do not use Claude Code.

# Make it a habit: Hooks and skills always tested.

When hooks, skills or settings change, your agent picks the cheapest test tier, writes a unit or deterministic test, runs npx vigiles test --no-skip in CI and checks eval locks with vigiles eval --check. Real-model evals run locally. Locks are the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** harness files changed (event; GitHub Actions; `push touches .claude/, hooks/, skills/ or CLAUDE.md`)
- **Verification:** harness tests and locks pass. Hard checks: npx vigiles test --no-skip passes; vigiles eval --check finds no stale lock; each changed hook has at least one runHook test. On fail: notify, max 1 retries.
- **Memory:** eval lock files at `.vigiles/eval-locks/`. Read first: recorded eval results and the inputs they were hashed from.

## Steps

1. **Pick the tier.** Choose unit, deterministic or eval from the tier table, cheapest first.
2. **Install vigiles.** Add vigiles as a dev dependency if it is missing.
3. **Find the surface.** Check .claude/settings.json, .claude-plugin/plugin.json, hooks/hooks.json and skills/.
4. **Write the test.** Follow references/writing-tests.md for the chosen tier.
5. **Run in CI.** Run npx vigiles test --no-skip so skipped tiers fail.
6. **Keep locks fresh.** After a local eval, run vigiles eval --update and commit the lock; CI runs --check.

Stop rule: Stops after one harness surface per run; real-model evals run only locally, never in CI.

## Permissions

- Writes: **/*.harness.mjs, **/*.harness.ts, .vigiles/eval-locks/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.vigiles/eval-locks/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: harness files changed. Verification: harness tests and locks pass. Memory: .vigiles/eval-locks/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
