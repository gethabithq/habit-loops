---
name: test-driven-development
title: Test-Driven Development skill
repo: obra/superpowers
license: MIT
url: https://gethabit.dev/skills/obra/test-driven-development
---

# Test-Driven Development skill

The test-driven development skill makes your coding agent write a failing test, watch it fail, then write the least code to pass. For developers who want agent code they can trust.

- Install the skill: `npx skills add obra/superpowers --skill test-driven-development`
- Source: https://github.com/obra/superpowers/tree/HEAD/skills/test-driven-development
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you add a new feature; you fix a bug; you change behavior or refactor.
Skip it when: it is a throwaway prototype; the file is generated code or config.

# Make it a habit: Every change starts with a test.

When a feature or bugfix task starts, your agent writes one failing test, watches it fail, writes the least code to pass, and runs the full suite. Code written before its test gets deleted. A log keeps which tests failed first and why.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** feature or bugfix task (event; Claude Code routine or GitHub Actions; `issue labelled feature or bug`)
- **Verification:** red then green. Hard checks: new test fails before the code exists; the failure is the expected one, not an error; new test passes after the code; the full project test command passes; output has no errors or warnings. On fail: retry, max 2 retries.
- **Memory:** red and green log at `loops/test-driven-development-loop/log.md`. Read first: tests written last run and failures named in the report.

## Steps

1. **Write failing test.** Write one small test with a clear name for one behavior.
2. **Watch it fail.** Run it, for example with npm test, and confirm it fails because the feature is missing.
3. **Write minimal code.** Write the simplest code that makes the test pass and nothing more.
4. **Run the full suite.** Run the project's test command, such as pytest, npm test or cargo test, and report every failure by name.
5. **Refactor.** Clean up names and duplication while all tests stay green.
6. **Ask on exceptions.** For prototypes, generated code or config files, ask your human partner first.

Stop rule: Stops after one behavior per cycle and one task per run.

## Permissions

- Writes: src/**, tests/**, loops/test-driven-development-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/test-driven-development-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: feature or bugfix task. Verification: red then green. Memory: loops/test-driven-development-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
