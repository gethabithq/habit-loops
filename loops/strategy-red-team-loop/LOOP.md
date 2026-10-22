---
name: strategy-red-team
title: Strategy Red-Team skill
repo: phuryn/pm-skills
license: MIT
url: https://gethabit.dev/skills/phuryn/strategy-red-team
---

# Strategy Red-Team skill

The strategy red-team skill attacks the load-bearing assumptions of a PRD, roadmap or strategy, ranks failure modes and returns the cheapest test and kill criterion for each, for product managers and founders before a big decision.

- Install the skill: `npx skills add phuryn/pm-skills --skill strategy-red-team`
- Source: https://github.com/phuryn/pm-skills/tree/HEAD/pm-execution/skills/strategy-red-team
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Stress-testing a plan or strategy; Preparing a doc for executive review; Challenging the key assumptions.
Skip it when: You want a full risk register; The plan is not written down yet.

# Make it a habit: Every plan gets attacked first.

When a PRD, roadmap or strategy doc changes, your agent red-teams it: it finds the load-bearing claims, attacks their strongest form, ranks failure modes and gives a cheapest test and kill criterion for each. The log tracks which assumptions were tested.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** plan document changed (event; Claude Code routine or GitHub Actions; `a PRD, roadmap or strategy document is added or edited`)
- **Verification:** format check + critic. Hard checks: output has 3 to 5 ranked kill-assumptions; each kill-assumption has fails if, evidence, kill criterion and cheapest test; sections for well-reasoned parts and unassessed gaps exist. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** assumption test board at `loops/strategy-red-team-loop/board.md`. Read first: kill-assumptions from earlier runs and whether their cheapest tests were done.

## Steps

1. **Extract claims.** List what the plan asserts and keep only the claims that would sink it if false.
2. **Steelman and attack.** State the best case for each load-bearing claim, then attack that version.
3. **Write failure modes.** Phrase each risk as a concrete, falsifiable Fails if condition.
4. **Rank them.** Order by impact, likelihood of being wrong and how cheap the test is.
5. **Self-refute.** Say plainly where the plan holds up and never invent a weakness.
6. **Give next actions.** For each surviving assumption add evidence to get this week, a kill criterion and the cheapest test.
7. **Format and log.** Write the ranked red-team report and add open tests to the board.

Stop rule: One plan per run, at most five kill-assumptions, one retry.

## Permissions

- Writes: loops/strategy-red-team-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/strategy-red-team-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: plan document changed. Verification: format check + critic. Memory: loops/strategy-red-team-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
