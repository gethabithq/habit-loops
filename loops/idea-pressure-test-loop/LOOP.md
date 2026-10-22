---
name: idea-validator
title: Idea Validator skill
repo: buildgreatproducts/builder-os
license: MIT
url: https://gethabit.dev/skills/buildgreatproducts/idea-validator
---

# Idea Validator skill

Idea validator is a BuilderOS skill for founders that pressure-tests a product idea for fatal flaws, real pain, competition, first customers and a 2-week MVP test, then gives a strong, weak or pivot verdict.

- Install the skill: `npx skills add buildgreatproducts/builder-os --skill idea-validator`
- Source: https://github.com/buildgreatproducts/builder-os/tree/HEAD/skills/idea-validator
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want your idea stress-tested; You need a 2-week MVP test; You doubt the problem is real.
Skip it when: You have no idea yet; You already validated with customers.

# Make it a habit: A blunt verdict on every idea.

Your agent pressure-tests a product idea: core assumption, ranked fatal flaws, problem reality, competition, first 10 customers, a 2-week MVP test, a scorecard and a strong, weak or pivot verdict. It writes docs/validation-report.md and re-runs after new discovery.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** idea file changes (event; Claude Code; `event: docs/product-idea.md updated or new discovery`)
- **Verification:** report written, verified. Hard checks: docs/validation-report.md exists after the write; the report has one verdict: Strong, Weak or Pivot required; the scorecard has six rows scored 1 to 5; Candidates considered is preserved unchanged. On fail: stop, max 0 retries.
- **Memory:** validation report at `docs/validation-report.md`. Read first: the last verdict and what changed since.

## Steps

1. **Read the idea.** Read docs/product-idea.md, or ask for idea, customer and desired action.
2. **Find the core.** State the one assumption that must be true.
3. **Find flaws.** List up to three fatal flaws by severity, each with a fast test.
4. **Test the market.** Write problem reality, competition map, first 10 customers and the MVP test.
5. **Score and judge.** Fill the six-row scorecard and give a Strong, Weak or Pivot verdict.
6. **Check direction.** Ask the founder the direction questions the findings raise.
7. **Write and hand off.** Apply agreed edits, write the report and point to Product Planner or Idea Generator.

Stop rule: Stops after one validation per run.

## Permissions

- Writes: docs/validation-report.md, docs/product-idea.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/validation-report.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: idea file changes. Verification: report written, verified. Memory: docs/validation-report.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
