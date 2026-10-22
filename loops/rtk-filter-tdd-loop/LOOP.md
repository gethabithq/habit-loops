---
name: tdd-rust
title: RTK TDD Rust skill
repo: rtk-ai/rtk
license: Apache-2.0
url: https://gethabit.dev/skills/rtk-ai/tdd-rust
---

# RTK TDD Rust skill

The RTK TDD Rust skill enforces red-green-refactor for RTK filter development: real command fixtures, a 20% token savings test, insta snapshots, edge case tests and a fmt, clippy and test gate. For contributors to RTK.

- Install the skill: `npx skills add rtk-ai/rtk --skill tdd-rust`
- Source: https://github.com/rtk-ai/rtk/tree/HEAD/.claude/skills/tdd-rust
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You add a new RTK filter; You write tests for a filter; A filter test fails.
Skip it when: You work outside RTK; You change docs only.

# Make it a habit: Every new filter proves its savings.

For each new RTK filter, your agent captures a real fixture, writes failing snapshot, savings and edge case tests, implements the minimum filter, accepts the insta snapshot, wires it into main.rs and runs the fmt, clippy and test gate.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new filter requested (event; Claude Code routine; `task to implement a new RTK filter or command`)
- **Verification:** savings and gate pass. Hard checks: token savings test shows at least 20%; empty and malformed input tests do not panic; snapshot accepted with cargo insta review; cargo fmt --all, cargo clippy --all-targets and cargo test pass. On fail: retry, max 2 retries.
- **Memory:** real command fixtures at `tests/fixtures/`. Read first: existing <command>_raw.txt fixtures.

## Steps

1. **Capture a fixture.** Your agent saves real command output as tests/fixtures/<command>_raw.txt.
2. **Write red tests.** It writes snapshot, 20% savings, empty and malformed input tests and runs cargo test to see them fail.
3. **Go green.** It writes the minimum filter_<cmd> returning Result<String>.
4. **Accept the snapshot.** It runs the snapshot test and cargo insta review.
5. **Wire it in.** It adds a run() with fallback and registers it in the main.rs Commands enum.
6. **Run the gate.** It runs cargo fmt --all, cargo clippy --all-targets and cargo test.

Stop rule: Stops after one filter and 2 gate retries per run.

## Permissions

- Writes: src/**, tests/fixtures/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`tests/fixtures/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new filter requested. Verification: savings and gate pass. Memory: tests/fixtures/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
