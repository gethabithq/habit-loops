---
name: code-review-and-quality
title: Code Review and Quality skill
repo: addyosmani/agent-skills
license: MIT
url: https://gethabit.dev/skills/addyosmani/code-review-and-quality
---

# Code Review and Quality skill

The code review and quality skill gives your agent a five-axis review for correctness, readability, architecture, security and performance, with severity labels and test checks, for teams who review code from people or agents.

- Install the skill: `npx skills add addyosmani/agent-skills --skill code-review-and-quality`
- Source: https://github.com/addyosmani/agent-skills/tree/HEAD/skills/code-review-and-quality
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Before you merge a pull request; After another agent wrote code; After a bug fix with a regression test.
Skip it when: The change is a full file deletion only; You need a deep security audit alone.

# Make it a habit: Every PR reviewed before merge.

When a pull request opens, your agent reviews it on five axes: correctness, readability, architecture, security and performance. It tests the tests by flipping one condition, labels each finding by severity, and checks that tests and build pass. A log keeps repeat findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened, pull_request.synchronize`)
- **Verification:** tests, build, your call. Hard checks: tests pass; build succeeds; a flipped condition makes the suite fail, or a missing test is named; every finding carries a severity label; no Critical finding left open. On fail: notify, max 0 retries.
- **Memory:** review findings log at `loops/five-axis-review-loop/log.md`. Read first: findings that came back in earlier reviews of this repo.

## Steps

1. **Understand intent.** Your agent reads what the change should do and which task it serves.
2. **Review tests first.** It inverts one new condition, runs the suite and restores the file to see if tests catch it.
3. **Five-axis pass.** It walks each file for correctness, readability, architecture, security and performance, using security-and-hardening and performance-optimization for depth.
4. **Label findings.** It marks each one Critical, required, Nit, Optional or FYI, most important first.
5. **Check dependencies.** For upgrades it reads the changelog, the lockfile diff and npm audit.
6. **Ask about dead code.** It lists code that is now unused and asks you before anything is removed.
7. **Verify.** Tests and build must pass, and a person makes the final merge call.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/five-axis-review-loop/**
- Network: api.github.com
- Sends: review comment on the pull request
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/five-axis-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: tests, build, your call. Memory: loops/five-axis-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
