---
name: find-bugs
title: Find Bugs skill
repo: getsentry/skills
license: Apache-2.0
url: https://gethabit.dev/skills/getsentry/find-bugs
---

# Find Bugs skill

The find bugs skill from Sentry reviews local branch changes for bugs, security holes and quality issues with a full diff read and a security checklist, then reports verified findings. For developers who want a review before merge.

- Install the skill: `npx skills add getsentry/skills --skill find-bugs`
- Source: https://github.com/getsentry/skills/tree/HEAD/skills/find-bugs
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You want a review of your branch; You need a security pass on changes; You audit code before merge.
Skip it when: You want automatic fixes; You only need style checks.

# Make it a habit: Find bugs before branches merge.

When a pull request opens, your agent reads the full branch diff, maps the attack surface, walks the security checklist for every file, verifies each issue and reports findings by severity. It changes nothing; you decide what to fix.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened`)
- **Verification:** full coverage, you decide. Hard checks: every changed file is listed as fully read; every checklist item is marked clean or flagged; each finding has file, line and evidence. On fail: notify, max 0 retries.
- **Memory:** findings per branch at `loops/branch-bug-hunt-loop/findings.md`. Read first: past findings and which you chose to fix.

## Steps

1. **Get the diff.** Your agent runs git diff against the default branch from gh repo view and reads every changed line.
2. **Map the surface.** It lists user inputs, queries, auth checks, session state, external calls and crypto.
3. **Run the checklist.** It checks injection, XSS, auth, IDOR, CSRF, races, sessions, crypto, disclosure, DoS and logic.
4. **Verify.** It checks if each issue is handled elsewhere or already tested.
5. **Audit itself.** It lists files read, checklist results and areas it could not verify.
6. **Report.** It reports findings by severity with a concrete fix, and you pick what to address.

Stop rule: Stops after one branch per run.

## Permissions

- Writes: loops/branch-bug-hunt-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/branch-bug-hunt-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: full coverage, you decide. Memory: loops/branch-bug-hunt-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
