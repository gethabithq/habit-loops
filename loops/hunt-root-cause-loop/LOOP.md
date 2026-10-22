---
name: hunt
title: Hunt skill
repo: tw93/Waza
license: MIT
url: https://gethabit.dev/skills/tw93/hunt
---

# Hunt skill

The hunt skill finds the root cause of an error, crash or regression before any fix, then proves the fix with a repro and a regression test. It is for developers who keep patching symptoms.

- Install the skill: `npx skills add tw93/Waza --skill hunt`
- Source: https://github.com/tw93/Waza/tree/HEAD/plugins/waza/skills/hunt
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Something errors, crashes or regressed; A bug came back after a fix; Something used to work after an update.
Skip it when: You want a code review; You are building a new feature.

# Make it a habit: Find the cause before fixing.

When a test fails on the main branch, your agent runs hunt: it states one testable root cause, proves it with a probe, fixes only within scope, sweeps the repo for the same pattern and adds a regression test that ran red then green. Each run is logged.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** test fails on main (event; GitHub Actions or Claude Code routine; `workflow_run.conclusion == failure on main`)
- **Verification:** red-green test + sweep. Hard checks: the targeted test or build passes after the fix; the regression test fails on the unfixed code; every grep match in the sibling sweep has a written verdict; the root cause names a file, line or condition. On fail: stop, max 2 retries.
- **Memory:** root cause log at `loops/hunt-root-cause-loop/log.md`. Read first: past root causes, ruled-out hypotheses and open sibling risks.

## Steps

1. **Collect symptoms.** Your agent lists every observed symptom and builds a small repro, reliably for timing issues.
2. **State the cause.** It writes one sentence that names the file, function, line or condition, with the evidence.
3. **Confirm or discard.** It runs the one probe that would fail if the idea were wrong, and drops a disproven idea.
4. **Bisect if needed.** For something that used to work, it reads git diff first and bisects in a temporary worktree when the tree is dirty.
5. **Fix in scope.** Only when a fix was asked for, it changes the cause, never the symptom, and does not commit or push on its own.
6. **Sweep siblings.** It runs grep -rn for the same pattern and marks each match as same bug, safe, or unsure for you.
7. **Guard and report.** A regression test runs red then green, and the output block lists cause, fix, sweep and tests.

Stop rule: Stops after one failure per run; after three failed hypotheses it hands off as blocked.

## Permissions

- Writes: src/**, tests/**, loops/hunt-root-cause-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/hunt-root-cause-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: test fails on main. Verification: red-green test + sweep. Memory: loops/hunt-root-cause-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
