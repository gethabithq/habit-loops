---
name: testing
title: Testing skill
repo: tursodatabase/turso
license: MIT
url: https://gethabit.dev/skills/tursodatabase/testing
---

# Testing skill

The testing skill from the Turso repo tells agents which test type to use, how to run them and how to write .sqltest, TCL and Rust integration tests, including converting TCL tests to .sqltest. For Turso contributors.

- Install the skill: `npx skills add tursodatabase/turso --skill testing`
- Source: https://github.com/tursodatabase/turso/tree/HEAD/.claude/skills/testing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: adding a test for a functional change; converting TCL tests to .sqltest; choosing between sqltest, Rust and fuzz tests.
Skip it when: you test an app built on Turso; you work outside the Turso repo.

# Make it a habit: Legacy TCL tests move to sqltest.

Each night your agent converts a few legacy TCL .test files to .sqltest with the test runner's convert command, fixes what the converter missed, adjusts expected results to the generated database and runs them. A board tracks which files are done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly test conversion (schedule; Claude Code routine or cron; `0 3 * * *`)
- **Verification:** converted tests pass. Hard checks: make -C sqlite/conformance run-rust passes for the new files; SQL statements match the original TCL tests; no converter warnings left unresolved; converted test count is above zero. On fail: retry, max 2 retries.
- **Memory:** conversion board at `loops/sqltest-conversion-loop/board.md`. Read first: TCL files still to convert and files with open warnings.

## Steps

1. **Pick TCL files.** Your agent takes the next legacy files from testing/ off the board.
2. **Run the converter.** It runs cargo run -- convert <TCL_test_path> -o <out_dir> from the test runner.
3. **Fix warnings by hand.** Where the converter warns, it writes the missing parts by hand, such as unrolled loops.
4. **Run the new tests.** It runs make -C sqlite/conformance run-rust on the converted files.
5. **Adjust expected output.** It updates expected results for the seeded database, never the SQL itself.
6. **Update the board.** It marks files converted or lists what still fails.

Stop rule: Stops after five TCL files per run.

## Permissions

- Writes: sqlite/conformance/sqlite-sqltests/**, loops/sqltest-conversion-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/sqltest-conversion-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly test conversion. Verification: converted tests pass. Memory: loops/sqltest-conversion-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
