---
name: code-quality
title: Code Quality Guide skill
repo: tursodatabase/turso
license: MIT
url: https://gethabit.dev/skills/tursodatabase/code-quality
---

# Code Quality Guide skill

The Code Quality Guide skill gives correctness rules and Rust patterns for a production database: assert invariants, crash over corrupt, exhaustive matches, no over-engineering and careful index ordering. For developers on the Turso codebase.

- Install the skill: `npx skills add tursodatabase/turso --skill code-quality`
- Source: https://github.com/tursodatabase/turso/tree/HEAD/.claude/skills/code-quality
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: reviewing Rust changes for correctness; checking invariants and error handling; checking index mutation ordering.
Skip it when: the code is not Rust; the project is not correctness-critical.

# Make it a habit: Changes that crash, never corrupt.

When Rust changes, your agent reviews the diff against the code-quality rules: no silent else branches, asserts on invariants, exhaustive matches, no over-engineering, and index mutation order checked against SQLite. A run log keeps findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Rust code changes (event; GitHub Actions or Claude Code routine; `pull_request opened or updated`)
- **Verification:** rules checked on diff. Hard checks: no else branch silently ignores a shouldn't-happen case; invalid states that risk data integrity assert or return an error; pattern matches are exhaustive; comments are only rust SAFETY comments. On fail: notify, max 1 retries.
- **Memory:** review findings log at `loops/rust-correctness-review-loop/run-log.md`. Read first: prior findings on the changed files.

## Steps

1. **Read the diff.** Your agent reads the Rust change set to review.
2. **Check correctness.** It flags workarounds, swallowed errors and continuing in an invalid state, preferring a crash to corruption.
3. **Check Rust patterns.** It checks for exhaustive matches, enums over sentinels and illegal states made unrepresentable.
4. **Check if-statements.** It flags an else branch that should never be hit and suggests assert, an error or unreachable.
5. **Check over-engineering.** It flags features beyond what was asked, needless abstractions and comments on unchanged code.
6. **Check index order.** On index inserts, deletes or conflict resolution it checks the ordering against SQLite.

Stop rule: Stops after one change set per run, with at most one re-scan.

## Permissions

- Writes: loops/rust-correctness-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/rust-correctness-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Rust code changes. Verification: rules checked on diff. Memory: loops/rust-correctness-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
