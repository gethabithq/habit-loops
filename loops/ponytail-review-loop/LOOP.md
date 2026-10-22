---
name: ponytail-review
title: Ponytail Review skill
repo: DietrichGebert/ponytail
license: MIT
url: https://gethabit.dev/skills/dietrichgebert/ponytail-review
---

# Ponytail Review skill

The ponytail review skill makes your agent review a diff like the developer on call: bugs, security, real load, missing tests, speed and code to delete, each with a concrete case and the smallest fix. For developers who want plain, actionable reviews.

- Install the skill: `npx skills add DietrichGebert/ponytail --skill ponytail-review`
- Source: https://github.com/DietrichGebert/ponytail/tree/HEAD/.openclaw/skills/ponytail-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a review before merging; A change touches shared functions; You want to know what code can be deleted.
Skip it when: You only want style comments; You want the agent to change code directly.

# Make it a habit: Every change reviewed before merge.

When a pull request opens, your agent reads the diff and the code around it, then reports bugs, security risks, load problems, missing tests, slowness and code to delete. Each finding names a case and a fix. It logs the verdict per pull request.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened or pull_request.synchronize`)
- **Verification:** report format check. Hard checks: report starts with What this change does:; every finding has What this is, Problem, Fix and If we skip it; every finding names a file and line range; report ends with a Verdict: line; no code was changed by the review. On fail: retry, max 1 retries.
- **Memory:** review verdict log at `loops/ponytail-review-loop/log.md`. Read first: past verdicts and findings still open on this branch.

## Steps

1. **Understand first.** Read the diff, callers, called functions, tests and README, and find the expected load.
2. **Look for problems.** Check for bugs, risks, scale issues, missing tests, slowness and lean cuts in that order.
3. **Confirm each case.** Keep only findings with a concrete input that goes wrong, and skip marked shortcut: comments within their limit.
4. **Write the report.** Group findings into must fix, should fix and nice to have, numbered across groups.
5. **Give the verdict.** End with the verdict, possible lean line savings and anything not checked.

Stop rule: Stops after one pull request per run and one retry if the report format fails.

## Permissions

- Writes: loops/ponytail-review-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ponytail-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: report format check. Memory: loops/ponytail-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
