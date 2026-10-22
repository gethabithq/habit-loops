---
name: om-auto-create-pr
title: Auto Create PR skill
repo: open-mercato/skills
license: MIT
url: https://gethabit.dev/skills/open-mercato/om-auto-create-pr
---

# Auto Create PR skill

Auto Create PR (the om-auto-create-pr skill) runs a free-form task end to end: a Progress-tracked plan, phase-by-phase commits in an isolated worktree, a validation gate, a review pass and a labelled PR. For teams on the open-mercato agent pipeline.

- Install the skill: `npx skills add open-mercato/skills --skill om-auto-create-pr`
- Source: https://github.com/open-mercato/skills/tree/HEAD/skills/om-auto-create-pr
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: shipping a task brief as a PR; running an autonomous coding task; implementing a resolved spec.
Skip it when: you have no agent pipeline configured; the change is a trivial one-off edit.

# Make it a habit: Task brief shipped as a PR

On a task brief, your agent claims a run slot, drafts a Progress-tracked plan, implements phase by phase in an isolated worktree, runs the validation gate and review pass, and opens a labelled PR. The plan file holds progress.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you give a task brief (manual; Claude Code routine; `/om-auto-create-pr <brief>`)
- **Verification:** gate and review pass. Hard checks: the run slot is claimed before any write; the plan has the Progress section in the exact format; every validation.commands command exits zero; the om-auto-review-pr pass reaches a clean verdict. On fail: stop, max 1 retries.
- **Memory:** execution plan at `$RUNS_DIR/<date>-<slug>.md`. Read first: the plan's goal, scope and Progress section.

## Steps

1. **Claim the slot.** Your agent confirms no other run owns the slot, or hands off to the resume skill on re-entry.
2. **Parse the brief.** It captures the goal, affected areas and scope, and reads only operator-passed skill URLs.
3. **Triage.** It reads the repo's agent instructions and reduces the brief to a goal, scope and explicit non-goals.
4. **Draft the plan.** It writes a lightweight plan with phases, steps and the exact Progress section, routing long plans to the loop engine.
5. **Worktree and plan commit.** It creates an isolated worktree, commits the plan and opens a draft PR for visibility.
6. **Implement.** It implements phase by phase with tests, ticking Progress and pushing after each phase.
7. **Gate, review, finalize.** It runs the validation gate, the review pass, normalizes labels and flips the PR ready at completion.

Stop rule: Stops after one task per run; it stops if the gate or review cannot pass.

## Permissions

- Writes: $RUNS_DIR/**, a fresh feat/ or fix/ branch in an isolated worktree
- Network: github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`$RUNS_DIR/<date>-<slug>.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you give a task brief. Verification: gate and review pass. Memory: $RUNS_DIR/<date>-<slug>.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
