---
name: effect
title: Effect skill
repo: kitlangton/skills
license: MIT
url: https://gethabit.dev/skills/kitlangton/effect
---

# Effect skill

The effect skill helps TypeScript developers build production apps with Effect v4: services, layers, schemas, config, schedules, caches, streams, HTTP clients and tests.

- Install the skill: `npx skills add kitlangton/skills --skill effect`
- Source: https://github.com/kitlangton/skills/tree/HEAD/skills/effect
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write Effect v4 services; You model data with Effect Schema; You test Effect code.
Skip it when: You are on Effect v3 with no upgrade plan; You do not use Effect.

# Make it a habit: Effect code follows v4 defaults.

On every pull request that touches Effect code, your agent reads the matching branch references and checks the core defaults and do-nots: Effect.fn on services, Schema.TaggedError, Config over process.env, no casts. A log keeps open issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Effect code changes (event; GitHub Actions or Claude Code routine; `pull_request touches files importing effect`)
- **Verification:** tests and do-nots. Hard checks: tests pass; no as any or non-null assertions added; no direct process.env reads in application logic; no Effect.sleep added to tests. On fail: notify, max 0 retries.
- **Memory:** effect review log at `loops/effect-v4-review-loop/run-log.md`. Read first: open issues and the pinned effect version.

## Steps

1. **Check sources.** Read the nearest AGENTS.md and the pinned effect version first.
2. **Pick branches.** Read only the references the change touches, such as references/SCHEMA.md or references/TESTING.md.
3. **Check defaults.** Compare services, schemas, config, schedules and streams with the core defaults.
4. **Check do-nots.** Flag casts, Schema.Class defaults, blind Layer.mergeAll and hand-rolled caches.
5. **Run tests.** Run the tests and log findings.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/effect-v4-review-loop/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/effect-v4-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Effect code changes. Verification: tests and do-nots. Memory: loops/effect-v4-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
