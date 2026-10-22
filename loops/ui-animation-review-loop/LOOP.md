---
name: ui-animation
title: UI Animation skill
repo: mblode/agent-skills
license: MIT
url: https://gethabit.dev/skills/mblode/ui-animation
---

# UI Animation skill

The ui animation skill helps frontend developers build, review and measure interface motion: springs, gestures, scroll effects, easing curves fitted from recordings and sparse interface sound.

- Install the skill: `npx skills add mblode/agent-skills --skill ui-animation`
- Source: https://github.com/mblode/agent-skills/tree/HEAD/skills/ui-animation
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add or tune UI motion; You review animation code in a PR; You copy easing from a screen recording.
Skip it when: You pick palettes or typography; You audit a whole page's UI quality.

# Make it a habit: Smooth motion in every PR.

When a pull request changes motion code, your agent greps the diff for layout transitions and transition: all, checks the core motion rules, reviews against the ten standards with a Block or Approve verdict and logs repeat issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches animation code (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize with CSS or Motion changes`)
- **Verification:** diff grep, review verdict. Hard checks: no transition on width, height, top or left in the diff; no transition: all in the diff; no new framer-motion import for new work; will-change is not set permanently; the review ends with a Block or Approve verdict. On fail: notify, max 0 retries.
- **Memory:** animation review log at `loops/ui-animation-review-loop/log.md`. Read first: patterns flagged in earlier reviews.

## Steps

1. **Read the diff.** A pull request that changes motion code starts the run.
2. **Grep the diff.** The agent flags transitions on width, height, top or left and any transition: all.
3. **Check core rules.** It checks will-change use, reduced motion handling and new framer-motion imports.
4. **Review the motion.** It applies the ten standards in references/review-format.md and fills the Before/After/Why table.
5. **Give a verdict.** The review ends with a Block or Approve decision.
6. **Log the run.** The log keeps flagged patterns so repeat issues stand out next time.

Stop rule: Stops after one pull request per run, with no retries.

## Permissions

- Writes: loops/ui-animation-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ui-animation-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches animation code. Verification: diff grep, review verdict. Memory: loops/ui-animation-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
