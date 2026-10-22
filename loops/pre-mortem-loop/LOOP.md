---
name: pre-mortem
title: Pre-mortem skill
repo: phuryn/pm-skills
license: MIT
url: https://gethabit.dev/skills/phuryn/pre-mortem
---

# Pre-mortem skill

The pre-mortem skill helps product managers stress-test a PRD or launch plan. It imagines a failed launch, sorts risks into Tigers, Paper Tigers and Elephants, and writes action plans for blockers.

- Install the skill: `npx skills add phuryn/pm-skills --skill pre-mortem`
- Source: https://github.com/phuryn/pm-skills/tree/HEAD/pm-execution/skills/pre-mortem
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a launch is a few weeks away; a PRD needs a stress test; the team avoids hard questions.
Skip it when: there is no plan written yet; you need a post-launch incident review.

# Make it a habit: Catch launch risks while fixable.

When a PRD or launch plan changes, your agent runs a pre-mortem: it sorts risks into Tigers, Paper Tigers and Elephants, ranks Tigers by urgency and writes action plans. A check confirms the report file exists with all sections.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** launch plan changed (event; GitHub Actions or Claude Code routine; `push touching the PRD or launch plan file`)
- **Verification:** report sections all present. Hard checks: PreMortem-[product-name]-[date].md file exists; report has Tigers, Paper Tigers and Elephants sections; every Launch-Blocking Tiger has risk, mitigation, owner and due date. On fail: retry, max 1 retries.
- **Memory:** past pre-mortem reports at `loops/pre-mortem-loop/board.md`. Read first: the last pre-mortem and which launch-blocking Tigers are still open.

## Steps

1. **Read the plan.** Your agent reads the PRD or product plan and notes the market, assumptions and timeline.
2. **Imagine failure.** It pictures the launch two weeks out going badly and asks what was missed.
3. **Sort the risks.** Each risk becomes a Tiger, a Paper Tiger or an Elephant, with Tiger as the default when unsure.
4. **Rank the Tigers.** Tigers are marked Launch-Blocking, Fast-Follow or Track.
5. **Plan the fixes.** Every Launch-Blocking Tiger gets a mitigation, an owner role and a due date.
6. **Save the report.** The analysis is saved as PreMortem-[product-name]-[date].md and the board notes open blockers.

Stop rule: Stops after one plan per run and at most one retry.

## Permissions

- Writes: PreMortem-*.md, loops/pre-mortem-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pre-mortem-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: launch plan changed. Verification: report sections all present. Memory: loops/pre-mortem-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
