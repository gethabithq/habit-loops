---
name: spec-impl
title: Spec Impl skill
repo: klerith/fernando-skills
license: MIT
url: https://gethabit.dev/skills/klerith/spec-impl
---

# Spec Impl skill

Spec impl implements an approved spec: it validates the Approved state in any language, creates a branch named after the spec, and works the plan step by step with pauses to review each diff. For teams executing a spec they have approved.

- Install the skill: `npx skills add klerith/fernando-skills --skill spec-impl`
- Source: https://github.com/klerith/fernando-skills/tree/HEAD/skills/engineering/spec-impl
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You implement an approved spec; You want branch-per-spec work; You want step-by-step diff reviews.
Skip it when: The spec is still a draft; You want the spec designed, not built.

# Make it a habit: Approved specs implemented on their branch.

When you implement an approved spec, your agent confirms the state means Approved, switches to a branch named after the spec, shows the objective, scope, plan and criteria, then implements the plan one step at a time, pausing after each step for a diff review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you implement a spec (manual; Claude Code slash command; `run /spec-impl with the spec name`)
- **Verification:** approved-state gate and step pauses. Hard checks: the spec state means Approved before any work; the branch spec-NN-slug is active; each plan step pauses for the user's diff review; no commit is made unless the user asks. On fail: notify, max 0 retries.
- **Memory:** spec and branch at `specs/`. Read first: the spec file, its state and the plan steps.

## Steps

1. **Identify the spec.** Find the spec in specs/ from the number, slug or full name given.
2. **Validate the state.** Continue only if the state means Approved in any language; otherwise stop with the standard message.
3. **Create the branch.** Check the working tree, then create and switch to spec-NN-slug per the AutoCreateBranch flag.
4. **Show the summary.** Show the objective, scope, implementation plan and acceptance criteria before coding.
5. **Implement step by step.** Do one plan step, show the touched files, and pause for the diff review before the next.
6. **Finish.** After the last step, remind the user to verify the acceptance criteria and commit.

Stop rule: Stops after the plan steps of one spec are implemented.

## Permissions

- Writes: **
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`specs/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you implement a spec. Verification: approved-state gate and step pauses. Memory: specs/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
