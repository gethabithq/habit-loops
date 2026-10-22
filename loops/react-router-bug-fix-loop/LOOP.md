---
name: fix-bug
title: Fix Bug skill
repo: remix-run/react-router
license: MIT
url: https://gethabit.dev/skills/remix-run/fix-bug
---

# Fix Bug skill

The fix bug skill takes a React Router GitHub issue and works through it: reads the issue, checks the reproduction, writes a failing test, makes a minimal fix, runs tests, lint and typecheck, and prepares a PR. For React Router contributors.

- Install the skill: `npx skills add remix-run/react-router --skill fix-bug`
- Source: https://github.com/remix-run/react-router/tree/HEAD/.agents/skills/fix-bug
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You have a React Router bug issue; You need a failing test first; You prepare a fix PR.
Skip it when: You work outside the React Router repo; The issue is a feature request.

# Make it a habit: Fix reported bugs with tests.

When you hand over a React Router issue, your agent reads it with gh issue view, validates the reproduction, writes a failing test, makes the minimal fix and runs tests, lint and typecheck. It adds a change file and waits for your review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you pass an issue (manual; Claude Code; `fix-bug <GitHub issue URL>`)
- **Verification:** test fails, then passes. Hard checks: the new test fails before the fix; the new test passes after the fix; pnpm test packages/react-router/ passes; pnpm lint and pnpm typecheck pass; a change file exists in .changes. On fail: retry, max 2 retries.
- **Memory:** fix branch history at `loops/react-router-bug-fix-loop/run-log.md`. Read first: issues already fixed and their branches.

## Steps

1. **Check clean tree.** Your agent asks you to resolve local changes, then branches from main.
2. **Read the issue.** It reads the issue with gh issue view and notes version and mode.
3. **Validate reproduction.** It reads the linked sandbox or repo, or asks you for a reproduction.
4. **Write failing test.** It adds a Jest unit test or a Playwright integration test that fails.
5. **Implement the fix.** It makes the smallest change that fixes the root cause.
6. **Run all checks.** It runs the test, the package suite, pnpm lint and pnpm typecheck.
7. **Add change file.** It writes a patch, minor, major or unstable change file.
8. **Review then PR.** You review; only after your approval does it commit and open a PR to main.

Stop rule: Stops after one issue and at most two fix attempts per run.

## Permissions

- Writes: packages/**, integration/**
- Network: none
- Sends: pull request to main after approval
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-router-bug-fix-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you pass an issue. Verification: test fails, then passes. Memory: loops/react-router-bug-fix-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
