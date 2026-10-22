---
name: debugging
title: Debugging skill
repo: tursodatabase/turso
license: MIT
url: https://gethabit.dev/skills/tursodatabase/debugging
---

# Debugging skill

The debugging skill from the Turso repo shows agents how to debug tursodb: compare EXPLAIN bytecode with SQLite, trace with logging, run ThreadSanitizer stress tests, replay deterministic simulation seeds and measure stack use. For Turso contributors.

- Install the skill: `npx skills add tursodatabase/turso --skill debugging`
- Source: https://github.com/tursodatabase/turso/tree/HEAD/.claude/skills/debugging
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: tursodb results differ from SQLite; a concurrency bug needs a seed; checking stack use of deep expressions.
Skip it when: you debug an app that only uses Turso; you work on another database.

# Make it a habit: Each mismatch traced to its layer.

When a query behaves differently in tursodb than in SQLite, your agent compares EXPLAIN bytecode from sqlite3 and tursodb to place the bug in code generation or in the VM and storage layer, then reproduces it and logs the finding.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** SQLite mismatch reported (event; GitHub Actions or Claude Code routine; `new issue reporting different results than sqlite3`)
- **Verification:** bytecode compared, bug reproduced. Hard checks: EXPLAIN output captured from sqlite3 and tursodb; bug layer named from the bytecode comparison; the query reproduces the mismatch with cargo run --bin tursodb; make test passes after any fix. On fail: notify, max 0 retries.
- **Memory:** compat triage log at `loops/turso-compat-triage-loop/log.md`. Read first: mismatches triaged before, their layer and simulator seeds.

## Steps

1. **Run in sqlite3.** Your agent runs EXPLAIN on the query with sqlite3 :memory:.
2. **Run in tursodb.** It runs the same EXPLAIN with cargo run --bin tursodb :memory:.
3. **Compare bytecode.** Different bytecode points to code generation; same bytecode with different results points to the VM or storage.
4. **Trace the core.** It reruns tests with RUST_LOG=none,turso_core=trace make test and reads testing/test.log.
5. **Reproduce with a seed.** For timing bugs it uses limbo_sim with -s <seed> or the concurrent simulator.
6. **Log the finding.** It records the query, layer, seed and next step in the log.

Stop rule: Stops after one reported mismatch per run.

## Permissions

- Writes: loops/turso-compat-triage-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/turso-compat-triage-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: SQLite mismatch reported. Verification: bytecode compared, bug reproduced. Memory: loops/turso-compat-triage-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
