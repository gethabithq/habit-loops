---
name: fix-errors
title: Fix Errors skill
repo: warpdotdev/common-skills
license: MIT
url: https://gethabit.dev/skills/warpdotdev/fix-errors
---

# Fix Errors skill

The fix errors skill helps developers fix compile errors, clippy and fmt failures, WASM errors and test failures in the warp Rust codebase with the narrowest useful command.

- Install the skill: `npx skills add warpdotdev/common-skills --skill fix-errors`
- Source: https://github.com/warpdotdev/common-skills/tree/HEAD/.agents/skills/fix-errors
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A Rust build or clippy run fails; WASM builds break on filesystem code; You need to run one test package.
Skip it when: The project is not the warp Rust codebase; You need a full design change, not a fix.

# Make it a habit: Red builds turned green, narrowly.

When a CI run fails on the warp Rust codebase, your agent reads the error, fixes one error type at a time with the narrowest command, then runs the matching cargo nextest tests and clippy and formats once. Fixes are logged by error type.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** CI check fails (event; GitHub Actions or Claude Code routine; `check_run.completed with conclusion failure`)
- **Verification:** tests and clippy pass. Hard checks: relevant cargo nextest run passes; applicable cargo clippy run has no warnings; cargo fmt -- --check passes; WASM clippy passes after WASM fixes. On fail: retry, max 2 retries.
- **Memory:** fixes by error type at `loops/rust-ci-fix-loop/run-log.md`. Read first: recent error types and the fixes that worked.

## Steps

1. **Read the error.** The agent reads the full message and checks if several errors share a cause.
2. **Fix one type.** It fixes one error type at a time, gating WASM-only code behind local_fs when needed.
3. **Check narrowly.** It runs the smallest useful cargo check or cargo nextest run -p for the package.
4. **Run clippy.** It runs the applicable clippy command, including WASM clippy for WASM errors.
5. **Format once.** It runs ./script/format once at the end and does not rerun tests after.

Stop rule: One failed CI run per run, at most two fix rounds; full presubmit only when required.

## Permissions

- Writes: crates/**, app/src/**, loops/rust-ci-fix-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/rust-ci-fix-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: CI check fails. Verification: tests and clippy pass. Memory: loops/rust-ci-fix-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
