---
name: create-prd
title: Create PRD skill
repo: phuryn/pm-skills
license: MIT
url: https://gethabit.dev/skills/phuryn/create-prd
---

# Create PRD skill

The create prd skill writes a lean product requirements document with eight sections, including segments and a six-part value proposition, for product managers and founders who need a team aligned fast.

- Install the skill: `npx skills add phuryn/pm-skills --skill create-prd`
- Source: https://github.com/phuryn/pm-skills/tree/HEAD/pm-execution/skills/create-prd
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a new feature or product; You need a short spec the team can read; You want to review an existing PRD.
Skip it when: You need a detailed technical design; The work is a small bug fix.

# Make it a habit: Every feature idea gets a PRD.

When a new feature idea comes in, your agent asks up to three questions, writes a lean 8-section PRD with create-prd, checks that segments and value propositions are there and logs each PRD so the next run knows what exists.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new feature idea filed (event; GitHub Actions or Claude Code routine; `issues.labeled == feature-idea`)
- **Verification:** your answers + section check. Hard checks: PRD-[product-name].md exists; Market Segments and Value Propositions sections are present; each segment has all six value proposition parts; no section contains TBD. On fail: notify, max 0 retries.
- **Memory:** PRDs written so far at `loops/lean-prd-loop/run-log.md`. Read first: PRDs already written and the open questions each one left.

## Steps

1. **Read the input.** Read the idea and any files the user attached to it.
2. **Ask the gaps.** If the problem, the users or the success metric is missing, ask up to three short questions and wait for answers.
3. **Research when useful.** Search the web for market, competitors or rules, and cite a source next to each claim that changes a decision.
4. **Write eight sections.** Write summary, contacts, background, objective, segments, value propositions, solution and release, short by default.
5. **Mark assumptions.** Put anything not known under assumptions and open questions instead of stating it as fact.
6. **Save and report.** Save PRD-[product-name].md and tell the user in one line which parts were skipped on purpose.
7. **Check and log.** Run the section checks and add the PRD with its open questions to the run log.

Stop rule: Stops after one PRD per run, or when the user has not answered the questions.

## Permissions

- Writes: PRD-*.md, loops/lean-prd-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/lean-prd-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new feature idea filed. Verification: your answers + section check. Memory: loops/lean-prd-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
