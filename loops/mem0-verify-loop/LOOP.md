---
name: mem0-test-integration
title: Mem0 Test Integration skill
repo: mem0ai/mem0
license: Apache-2.0
url: https://gethabit.dev/skills/mem0ai/mem0-test-integration
---

# Mem0 Test Integration skill

Mem0 Test Integration verifies a Mem0 integration on its branch: install, static checks, the repo's tests with the flag off and on, a real smoke call and an end-to-end flow, then a scorecard. For developers who ran mem0-integrate.

- Install the skill: `npx skills add mem0ai/mem0 --skill mem0-test-integration`
- Source: https://github.com/mem0ai/mem0/tree/HEAD/skills/mem0-test-integration
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: verifying a fresh Mem0 integration; checking the integration did not break existing tests; running a smoke and end-to-end flow.
Skip it when: there is no prior mem0-integrate run; you only want general project tests.

# Make it a habit: A Mem0 integration proven to run.

After /mem0-integrate, your agent installs dependencies, runs static checks, the repo's tests in two flag passes, a real smoke call and an end-to-end flow, then writes a scorecard. The scorecard files in .mem0-integration/ are the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** after mem0 integrate (event; GitHub Actions or Claude Code routine; `.mem0-integration/ exists on the branch`)
- **Verification:** two-pass tests and smoke. Hard checks: write-site imports the expected Mem0 surface; all pre-existing tests pass with the flag unset; new tests pass with the flag set; the smoke call stores and finds a memory; scorecard.json overall is pass. On fail: stop, max 0 retries.
- **Memory:** scorecard folder at `.mem0-integration/scorecard.json`. Read first: the last scorecard and product.json contract.

## Steps

1. **Check preconditions.** Your agent refuses unless .mem0-integration/ exists, the branch starts with mem0-integrate/ and the tree is clean.
2. **Read contract.** It reads product.json, plan.md and goal.md for language, product, flag and call sites.
3. **Install.** It installs dependencies by language and stops if they do not resolve.
4. **Static checks.** It checks the import surface, version range, types, lint and that the client is not built at module scope.
5. **Two test passes.** Pass A with the flag unset must be all green; Pass B with the flag set runs the new tests.
6. **Smoke test.** It makes one real add-then-search round trip with a disposable user id and cleans up.
7. **End to end.** If plan.md has an E2E recipe it runs the app and checks the stored memory appears in the output.
8. **Scorecard.** It writes scorecard.md and scorecard.json, prints the verdict and never patches source.

Stop rule: Stops after one verification per run; any failing step stops the run.

## Permissions

- Writes: .mem0-integration/**
- Network: docs.mem0.ai, raw.githubusercontent.com, github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.mem0-integration/scorecard.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: after mem0 integrate. Verification: two-pass tests and smoke. Memory: .mem0-integration/scorecard.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
