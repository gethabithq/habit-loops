---
name: rtk-tdd
title: RTK TDD skill
repo: rtk-ai/rtk
license: Apache-2.0
url: https://gethabit.dev/skills/rtk-ai/rtk-tdd
---

# RTK TDD skill

The rtk tdd skill enforces red-green-refactor test-driven development for Rust, with cfg(test) modules, Arrange-Act-Assert patterns and a fmt, clippy and test gate before commit. For Rust developers who want tests first.

- Install the skill: `npx skills add rtk-ai/rtk --skill rtk-tdd`
- Source: https://github.com/rtk-ai/rtk/tree/HEAD/.claude/skills/rtk-tdd
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You implement a Rust feature; You fix a Rust bug; You refactor Rust code.
Skip it when: The code is only CLI wiring; The project is not Rust.

# Make it a habit: Every Rust change starts red.

For each Rust task your agent writes a failing test in the same file, runs it red, writes the minimum code to go green, refactors and runs the fmt, clippy and test gate. A log keeps each red and green run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Rust task starts (event; Claude Code routine; `implementation, bug fix or refactor in a Rust repo`)
- **Verification:** red first, gate passes. Hard checks: the new test failed before the code change; cargo fmt --all --check passes; cargo clippy --all-targets passes; cargo test passes. On fail: retry, max 2 retries.
- **Memory:** red-green run log at `loops/rust-tdd-gate-loop/runs.md`. Read first: tests added last time and any allow attributes with reasons.

## Steps

1. **Write the test.** Your agent adds a test in the #[cfg(test)] mod tests of the same file.
2. **Run red.** It runs cargo test on that test and confirms it fails.
3. **Go green.** It writes only enough code to pass and reruns the test.
4. **Refactor.** It cleans up and reruns cargo test.
5. **Run the gate.** It runs cargo fmt, cargo clippy --all-targets and cargo test.

Stop rule: Stops after one task and 2 gate retries per run.

## Permissions

- Writes: src/**, loops/rust-tdd-gate-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/rust-tdd-gate-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Rust task starts. Verification: red first, gate passes. Memory: loops/rust-tdd-gate-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
