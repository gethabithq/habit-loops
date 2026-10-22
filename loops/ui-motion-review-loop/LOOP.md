---
name: emil-design-eng
title: Emil Design Eng skill
repo: emilkowalski/skills
license: MIT
url: https://gethabit.dev/skills/emilkowalski/emil-design-eng
---

# Emil Design Eng skill

The emil design eng skill gives your agent design engineering taste: motion, timing and the small details that make an interface feel right.

- Install the skill: `npx skills add emilkowalski/skills --skill emil-design-eng`
- Source: https://github.com/emilkowalski/skills
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build UI with animation; Your interface feels stiff.
Skip it when: You only change backend code.

# Make it a habit: Animations reviewed on every UI change.

When a pull request changes UI styles or components, your agent reviews them with emil-design-eng: easing, duration, transform origin, press states and reduced motion. A check scans the diff for known mistakes. The run log keeps open issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches UI code (event; GitHub Actions or Claude Code routine; `pull_request touching CSS or component files`)
- **Verification:** diff scan + table. Hard checks: no transition: all in changed CSS; no scale(0) entry animation in the diff; hover animations sit behind @media (hover: hover) and (pointer: fine); review output is one markdown table with Before, After and Why columns. On fail: notify, max 1 retries.
- **Memory:** motion issues log at `loops/ui-motion-review-loop/run-log.md`. Read first: open motion issues from earlier PRs.

## Steps

1. **Read the diff.** The agent reads the changed styles and components.
2. **Ask the questions.** For each animation it checks how often users see it, its purpose, its easing and its duration.
3. **Run the checklist.** It walks the review checklist, from ease-in on UI to keyframes on rapidly triggered elements.
4. **Write the table.** It writes one markdown table with Before, After and Why, one row per issue.
5. **Log.** Issues that stay open go into the run log for the next PR.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/ui-motion-review-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ui-motion-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches UI code. Verification: diff scan + table. Memory: loops/ui-motion-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
