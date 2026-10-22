---
name: studio-testing
title: Studio Testing skill
repo: supabase/supabase
license: Apache-2.0
url: https://gethabit.dev/skills/supabase/studio-testing
---

# Studio Testing skill

The studio testing skill gives the testing strategy for Supabase Studio: extract logic into .utils.ts files, test every permutation, use component tests only for complex UI and E2E tests for shared features. For Supabase Studio contributors.

- Install the skill: `npx skills add supabase/supabase --skill studio-testing`
- Source: https://github.com/supabase/supabase/tree/HEAD/.agents/skills/studio-testing
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You write tests for Studio code; You decide which test type to write; You review test coverage.
Skip it when: You work outside apps/studio; You only change docs.

# Make it a habit: Every Studio change gets right tests.

On each pull request in apps/studio, your agent walks the test decision tree, extracts pure logic into .utils.ts files, writes exhaustive unit tests, adds component tests only for complex UI and E2E tests for shared features, then runs the tests.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Studio code changes (event; GitHub Actions or Claude Code routine; `pull request touches apps/studio/`)
- **Verification:** tests pass, logic extracted. Hard checks: vitest passes; each new utility has tests for happy path, malformed and empty input; component tests mock APIs with addAPIMock, not vi.mock. On fail: retry, max 2 retries.
- **Memory:** coverage gap board at `loops/studio-test-coverage-loop/board.md`. Read first: components still holding logic that should be extracted.

## Steps

1. **Pick the test type.** Your agent runs the decision tree: unit, component or E2E.
2. **Extract logic.** It moves pure logic into a ComponentName.utils.ts file next to the component.
3. **Test every path.** It writes unit tests for valid, malformed, empty and edge inputs.
4. **Component tests.** For complex UI only, it uses customRender and addAPIMock.
5. **E2E for shared features.** For self-hosted and platform features it adds a test in e2e/studio/features/ with clicks and keys.
6. **Run tests.** It runs vitest and records any gaps left.

Stop rule: Stops after one pull request and 2 fix rounds per run.

## Permissions

- Writes: apps/studio/**, e2e/studio/**, loops/studio-test-coverage-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/studio-test-coverage-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Studio code changes. Verification: tests pass, logic extracted. Memory: loops/studio-test-coverage-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
