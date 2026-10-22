---
name: triage-ci-flake
title: Triage CI Flake skill
repo: payloadcms/payload
license: MIT
url: https://gethabit.dev/skills/payloadcms/triage-ci-flake
---

# Triage CI Flake skill

The triage ci flake skill gives agents a reproduce-first routine for e2e failures in CI: aggregate failing checks, rerun the exact Playwright test with dev and prod builds, fix and confirm with repeated runs. For Payload contributors.

- Install the skill: `npx skills add payloadcms/payload --skill triage-ci-flake`
- Source: https://github.com/payloadcms/payload/tree/HEAD/.agents/skills/triage-ci-flake
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: e2e tests fail on main after a merge; a test passes locally but fails in CI; a PR has several failing checks.
Skip it when: the failure is a unit test; you work outside the Payload repo setup.

# Make it a habit: Flaky e2e tests reproduced, then fixed.

When e2e tests fail on main after a merge, your agent reproduces each failing Playwright test with dev code, then with the prod build, fixes it only after reproduction, reruns it ten times and asks you before opening a PR.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** e2e fails on main (event; GitHub Actions or Claude Code routine; `CI e2e check fails on main after a PR merge`)
- **Verification:** ten green reruns. Hard checks: failure reproduced with pnpm dev or pnpm dev:prod before any fix; the fixed test passes ten runs in a row; the full suite file passes; prod build test passes if bundled code changed. On fail: stop, max 1 retries.
- **Memory:** flake triage log at `loops/ci-flake-triage-loop/log.md`. Read first: tests triaged before, whether they reproduced and the fix pattern used.

## Steps

1. **Aggregate failures.** Your agent reads the failing checks and lists suite, test name, error and file for each.
2. **Spot patterns.** It groups failures by shared selector, shared file or same suite.
3. **Reproduce with dev.** It frees port 3000, starts pnpm dev for the suite, waits with curl and runs only the failing test.
4. **Reproduce with prod.** If it passed, it runs pnpm prepare-run-test-against-prod and pnpm dev:prod, then the test again.
5. **Fix the cause.** It applies a condition-based fix that respects the playwright and payload eslint rules.
6. **Verify stability.** It reruns the test ten times and then the full suite file.
7. **Ask about the PR.** It shows a summary with files and results and asks you before creating a PR.

Stop rule: Stops after one failing suite per run; no fix without reproduction.

## Permissions

- Writes: loops/ci-flake-triage-loop/**, test/**
- Network: localhost:3000, github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ci-flake-triage-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: e2e fails on main. Verification: ten green reruns. Memory: loops/ci-flake-triage-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
