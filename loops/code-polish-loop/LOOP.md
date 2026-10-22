---
name: code-polish
title: Code Polish skill
repo: paulrberg/agent-skills
license: MIT
url: https://gethabit.dev/skills/paulrberg/code-polish
---

# Code Polish skill

The code polish skill simplifies and reviews changed code over a fixed scope, fixing evidence-backed defects by risk with language and security profiles, then verifies with lint, types and tests.

- Install the skill: `npx skills add paulrberg/agent-skills --skill code-polish`
- Source: https://github.com/paulrberg/agent-skills/tree/HEAD/skills/code-polish
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You just finished a change; You want a risk-ranked review; You want safe simplifications only.
Skip it when: The project is not a Git repository; You plan a large redesign.

# Make it a habit: Changed code ends up simpler.

When a pull request opens or updates, your agent fixes the scope to its changed files, simplifies with high confidence, reviews by risk profile and fixes evidence-backed defects. Lint, typecheck and targeted tests must pass.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR opened or updated (event; GitHub Actions or Claude Code routine; `pull_request.opened, pull_request.synchronize`)
- **Verification:** lint, types, tests pass. Hard checks: formatter and linter pass on touched files; typecheck passes; targeted tests pass; every selected profile exists under references/profiles/. On fail: stop, max 0 retries.
- **Memory:** polish report log at `loops/code-polish-loop/runs.md`. Read first: Open items and residual risks from the last report.

## Steps

1. **Fix the scope.** Take the changed files once, without lockfiles, generated outputs or vendored code.
2. **Simplify.** Apply only high-confidence simplifications that keep public contracts and behavior.
3. **Pick profiles.** Select each matching profile, such as security, typescript or shell, from references/profiles/.
4. **Review and fix.** Rank findings from CRITICAL to LOW and apply the smallest fix backed by evidence.
5. **Verify.** Run the narrowest formatter, lint, typecheck and targeted tests for the touched code.
6. **Report.** List Resolved and Open items with evidence, or a blocked report when parity cannot be shown.

Stop rule: Stops after one fixed scope per run, or earlier when a fix needs a redesign or contract change.

## Permissions

- Writes: loops/code-polish-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/code-polish-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR opened or updated. Verification: lint, types, tests pass. Memory: loops/code-polish-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
