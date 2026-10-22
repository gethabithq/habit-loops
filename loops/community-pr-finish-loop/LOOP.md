---
name: finish-line
title: Finish Line skill
repo: remix-run/react-router
license: MIT
url: https://gethabit.dev/skills/remix-run/finish-line
---

# Finish Line skill

The finish line skill brings a blocked React Router community pull request to a mergeable state by adding missing tests, change files or docs on the contributor branch, with maintainer approval before any push.

- Install the skill: `npx skills add remix-run/react-router --skill finish-line`
- Source: https://github.com/remix-run/react-router/tree/HEAD/.agents/skills/finish-line
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a community PR is stuck; a PR lacks a change file; tests or docs are missing.
Skip it when: the PR needs a big rewrite; the repository is not React Router.

# Make it a habit: Blocked community PRs get merged.

When you run /finish-line with a PR number, the agent finds what blocks a React Router community PR, adds the missing tests, change file or docs, shows you the content and pushes only after your OK. A log keeps each PR and its blocker.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** /finish-line with PR (manual; Claude Code routine; `/finish-line <pr-number-or-url>`)
- **Verification:** your OK + checks. Hard checks: gh pr checks shows no failed check; change file exists under packages/<package>/.changes/ when one was missing; git push to the PR branch succeeds. On fail: stop, max 0 retries.
- **Memory:** finished PR log at `loops/community-pr-finish-loop/log.md`. Read first: PRs already handled, their blockers and the test coverage decision.

## Steps

1. **Check local state.** Run git status --short --branch and git fetch origin main, and never stage unrelated files.
2. **Gather PR context.** Use gh pr view, gh pr checks and gh pr diff on the target PR in remix-run/react-router.
3. **Name the blocker.** Decide if the PR needs tests, a change file or docs, and ask you when the path is unclear.
4. **Judge test coverage.** Check if the diff changes behavior that can regress and if tests cover the affected modes.
5. **Make small fixes.** After gh pr checkout, add only the missing finish-line changes on the contributor branch.
6. **Ask for approval.** Show the file paths and full contents, then wait for your explicit OK to commit and push.
7. **Push and report.** Commit, push to the PR branch and report blocker, commit hash, validation and coverage decision.

Stop rule: Stops after one PR per run, and stops at once if git push fails.

## Permissions

- Writes: packages/<package>/.changes/, packages/react-router/lib/, loops/community-pr-finish-loop/
- Network: none
- Sends: commits pushed to the contributor PR branch
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/community-pr-finish-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: /finish-line with PR. Verification: your OK + checks. Memory: loops/community-pr-finish-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
