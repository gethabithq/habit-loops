---
name: allium
title: Allium skill
repo: juxt/allium
license: MIT
url: https://gethabit.dev/skills/juxt/allium
---

# Allium skill

The allium skill is a formal language and loop for specifying software behaviour: it captures intent in .allium files, generates integration and end-to-end tests, and drives spec, tests and code to agreement. For developers who want behaviour locked down before building.

- Install the skill: `npx skills add juxt/allium --skill allium`
- Source: https://github.com/juxt/allium/tree/HEAD/skills/allium
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: specifying a feature's behaviour precisely; generating tests from a spec; reconciling spec and code drift.
Skip it when: you want unit tests only; the task is a quick throwaway script.

# Make it a habit: Spec, tests and code all agree.

On a goal, your agent drives the Allium loop: gather context into a .allium spec, generate tests, implement, run tests and weed out drift, repeat until converged, then witness the claim. The .allium spec is the durable memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you give a goal (manual; Claude Code routine; `/allium <goal>`)
- **Verification:** tests, weed, witness. Hard checks: the .allium file passes CLI validation on every write; generated tests pass; weed reports no spec-to-code divergence; no open question remains unresolved. On fail: retry, max 2 retries.
- **Memory:** allium spec at `spec.allium`. Read first: the current .allium spec, open questions and the convergence ledger.

## Steps

1. **Gather context.** Your agent builds or extracts the spec with elicit from intent or distill from existing code.
2. **Generate tests.** It runs propagate to make integration and end-to-end tests, confirming new tests fail first in spec-first work.
3. **Implement.** It writes the application code, ordinary coding the spec and tests do not replace.
4. **Verify.** It runs the tests, then weed to find spec-to-code drift, then the CLI structural checks.
5. **Repeat.** It edits the spec with tend and re-propagates until the three artefacts agree.
6. **Witness.** An independent witness pass attests the convergence against ground truth, never weakening a test to pass.

Stop rule: Stops when tests pass, weed finds no divergence, no open question remains and witness attests; otherwise after 2 loop retries.

## Permissions

- Writes: **/*.allium, tests/**, source files
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`spec.allium`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you give a goal. Verification: tests, weed, witness. Memory: spec.allium. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
