---
name: review-animations
title: Review Animations skill
repo: emilkowalski/skills
license: MIT
url: https://gethabit.dev/skills/emilkowalski/review-animations
---

# Review Animations skill

The review animations skill has your agent review animation and motion code against ten strict standards and return a findings table with a Block or Approve verdict. For design engineers who care how UI motion feels.

- Install the skill: `npx skills add emilkowalski/skills --skill review-animations`
- Source: https://github.com/emilkowalski/skills/tree/HEAD/skills/review-animations
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a pull request adds transitions; UI motion feels sluggish; you want a strict motion review.
Skip it when: the diff has no motion code; you need new features written.

# Make it a habit: Every animation earns its place.

When a pull request changes motion code, your agent checks each animation against ten standards and returns a Before, After, Why table with a Block or Approve verdict.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes motion code (event; GitHub Actions or Claude Code routine; `pull_request touches transition, animation or motion code`)
- **Verification:** Block or Approve verdict. Hard checks: no transition: all; no scale(0) entrance; no ease-in on UI motion; no UI duration over 300ms without a reason; prefers-reduced-motion is handled for movement. Critic: claude-opus-5-5, pass at 17/20. On fail: notify, max 0 retries.
- **Memory:** motion findings log at `loops/review-animations-loop/log.md`. Read first: findings and verdicts from earlier reviews.

## Steps

1. **Find motion changes.** List animation and transition code in the diff and skip code that does not move.
2. **Apply ten standards.** Measure each animation against the ten standards and the escalation triggers.
3. **Pull exact values.** Take curves, durations and spring settings from STANDARDS.md, not from memory.
4. **Order the fixes.** Prefer delete, then reduce, then fix easing, origin, interruption, GPU, timing and polish.
5. **Write the table.** Return one Before, After, Why table with file:line for each finding.
6. **Give the verdict.** Group the rest by impact tier and end with Block or Approve.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/review-animations-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/review-animations-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes motion code. Verification: Block or Approve verdict. Memory: loops/review-animations-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
