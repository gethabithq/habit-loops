---
name: propagate
title: Propagate skill
repo: juxt/allium
license: MIT
url: https://gethabit.dev/skills/juxt/propagate
---

# Propagate skill

The propagate skill generates tests from Allium specifications: assertion, property-based and state machine tests mapped to real code, with every obligation reconciled, for teams that keep a spec as the source of truth.

- Install the skill: `npx skills add juxt/allium --skill propagate`
- Source: https://github.com/juxt/allium/tree/HEAD/skills/propagate
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a spec is ready and needs tests; checking test coverage against spec obligations; a spec changed and tests must follow.
Skip it when: the spec has entities but no rules yet; no spec exists.

# Make it a habit: Spec changes regenerate the tests.

When an .allium spec changes, your agent reads allium plan and allium model, maps spec constructs to code and generates tests. Tests must run and every obligation must be covered or reported. Hashes and the summary line go into the ledger.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** allium spec changed (event; GitHub Actions or Claude Code routine; `push paths include **/*.allium`)
- **Verification:** tests run, obligations covered. Hard checks: generated tests compile and run; every obligation maps to a test or a reported reason; summary line reads N obligations, M covered, K uncovered; a hash is recorded for each generated test file. On fail: retry, max 2 retries.
- **Memory:** allium loop ledger at `.allium-loop/<goal-slug>.json`. Read first: generated_test_hashes and the last reconciliation line.

## Steps

1. **Read the spec.** Your agent reads the spec and judges if it is mature enough, else suggests elicit or distill.
2. **Read obligations.** It loads the test obligations from allium plan and the domain model from allium model.
3. **Explore the codebase.** It finds the test framework, any PBT framework, fixtures and existing tests.
4. **Map to code.** It links each entity, rule and surface to the code that implements it.
5. **Generate tests.** It writes assertion, property-based and state machine tests in the project's conventions.
6. **Run tests.** It checks that the generated tests compile and run.
7. **Reconcile.** It covers gaps with at most two attempts per obligation and reports the rest.

Stop rule: Stops after one spec per run; at most 2 attempts per obligation, and stops when a full pass covers nothing new.

## Permissions

- Writes: tests/**, __tests__/**, .allium-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.allium-loop/<goal-slug>.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: allium spec changed. Verification: tests run, obligations covered. Memory: .allium-loop/<goal-slug>.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
