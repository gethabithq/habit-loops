---
name: no-mistakes
title: no-mistakes skill
repo: kunchenguid/no-mistakes
license: MIT
url: https://gethabit.dev/skills/kunchenguid/no-mistakes
---

# no-mistakes skill

The no-mistakes skill drives a local validation gate: intent, rebase, review, test, docs, lint, push, PR and CI, answering each gate and escalating judgment calls before changes reach the push target. For developers who want every change checked.

- Install the skill: `npx skills add kunchenguid/no-mistakes --skill no-mistakes`
- Source: https://github.com/kunchenguid/no-mistakes/tree/HEAD/skills/no-mistakes
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to ship a branch safely; You finish a task and want it validated; You run /no-mistakes.
Skip it when: The repo is not initialized for no-mistakes; You are on the default branch.

# Make it a habit: Ship branches only through the gate.

For every finished task, your agent commits on a feature branch, runs no-mistakes axi run with full intent, answers each gate (fixing auto-fix findings, escalating ask-user ones to you) until an outcome, then summarizes what was validated and fixed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** task committed on branch (event; Claude Code routine; `feature branch has new commits, or /no-mistakes`)
- **Verification:** pipeline outcome, your calls. Hard checks: outcome is checks-passed or passed; every gate finding is listed in --findings or --ignore; no code edited by hand while a run is active. On fail: notify, max 1 retries.
- **Memory:** pipeline outcome log at `loops/no-mistakes-gate-loop/runs.md`. Read first: last outcome, fixes table and branch_sync state.

## Steps

1. **Check scope.** Your agent inspects git status and commits only the task's changes on a feature branch.
2. **Check home.** It runs no-mistakes axi to see active runs and next steps.
3. **Run with intent.** It runs no-mistakes axi run --intent with the full user goal and decisions.
4. **Answer gates.** It responds with --action fix for auto-fix findings and approve for no-op ones.
5. **Escalate ask-user.** It relays each ask-user finding to you verbatim and responds with your decision.
6. **Handle outcome.** On checks-passed it hands you the PR; on failed it follows branch_sync and reruns.
7. **Summarize.** It lists what was validated and each fix the pipeline made.

Stop rule: Stops at the first outcome, with at most one fresh run after a failure.

## Permissions

- Writes: loops/no-mistakes-gate-loop/**
- Network: github.com
- Sends: pull request through the configured push target
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/no-mistakes-gate-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: task committed on branch. Verification: pipeline outcome, your calls. Memory: loops/no-mistakes-gate-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
