---
name: genshijin-review
title: Genshijin Review skill
repo: interfacex-co-jp/genshijin
license: MIT
url: https://gethabit.dev/skills/interfacex-co-jp/genshijin-review
---

# Genshijin Review skill

genshijin review is a skill that writes very short pull request review comments in Japanese: one line per finding with line, problem and fix, for developers who want review signal without filler.

- Install the skill: `npx skills add interfacex-co-jp/genshijin --skill genshijin-review`
- Source: https://github.com/interfacex-co-jp/genshijin/tree/HEAD/skills/genshijin-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review a pull request; You want one finding per line; Your team reads Japanese.
Skip it when: You want the agent to fix the code; You need approve or request-changes actions.

# Make it a habit: Short review comments on every PR.

When a pull request opens, your agent reviews the diff with genshijin review: one line per finding with location, problem and fix. A hard check rejects comments without a line number or with hedging words. A run log keeps past findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened`)
- **Verification:** comment format check. Hard checks: every comment starts with L<line> or <file>:L<line>; every comment has a severity prefix when severities mix; no hedging phrases left in comments; no code changes in the diff of the run. On fail: retry, max 1 retries.
- **Memory:** review log at `loops/genshijin-review-loop/log.md`. Read first: findings from earlier reviews of this repo.

## Steps

1. **Pick up PR.** A newly opened pull request starts the run.
2. **Read the diff.** The agent reads the changed lines and notes exact line numbers.
3. **Write findings.** Each finding gets one line with position, problem and a concrete fix.
4. **Tag severity.** Findings get a prefix for bug, risk, nit or question.
5. **Expand when needed.** Security and architecture objections get a normal paragraph with reasons.
6. **Check and log.** The format check runs, then the findings go into the review log.

Stop rule: Stops after one pull request per run and at most one retry.

## Permissions

- Writes: loops/genshijin-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/genshijin-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: comment format check. Memory: loops/genshijin-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
