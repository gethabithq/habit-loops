---
name: spec-driven-development
title: Spec-Driven Development skill
repo: addyosmani/agent-skills
license: MIT
url: https://gethabit.dev/skills/addyosmani/spec-driven-development
---

# Spec-Driven Development skill

The Spec-Driven Development skill by Addy Osmani makes your agent write a reviewed specification before any code, then plan, split into tasks and implement with a human gate at each phase. For teams starting features with unclear requirements.

- Install the skill: `npx skills add addyosmani/agent-skills --skill spec-driven-development`
- Source: https://github.com/addyosmani/agent-skills/tree/HEAD/skills/spec-driven-development
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a new project or feature; Requirements are vague or incomplete; The change touches many files or modules.
Skip it when: It is a one-line fix or typo; The requirement is already clear and self-contained.

# Make it a habit: No code before an approved spec.

When a new feature starts, your agent lists its assumptions, asks you questions and writes a spec with six core areas, then stops for your approval. After each approval it moves one phase on: plan, tasks, implement. The spec file stays the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new feature request (event; Claude Code routine or GitHub Actions; `issues.opened with a feature request, or you start a feature in a session`)
- **Verification:** spec check + your approval. Hard checks: spec covers objective, commands, project structure, code style, testing strategy and boundaries; success criteria are listed and testable; boundaries have Always, Ask first and Never tiers; spec is saved to a file in the repo; run ends after saving the spec, before any plan or code. On fail: notify, max 0 retries.
- **Memory:** spec and task files at `SPEC.md`. Read first: the current spec, its open questions and tasks/plan.md.

## Steps

1. **Scope check.** If the request bundles several separately testable capabilities, propose a capability map with module ids and build order for your review.
2. **State assumptions.** List what the agent assumes and ask you clarifying questions until the requirements are concrete.
3. **Write the spec.** Cover the six core areas, success criteria and open questions, save it, and stop for your approval.
4. **Plan.** After approval, follow planning-and-task-breakdown and save the plan to tasks/plan.md.
5. **Tasks.** Record small tasks with acceptance criteria and a verify step in tasks/todo.md, then wait for your review.
6. **Implement.** Build tasks one by one with incremental-implementation, test-driven-development and context-engineering.
7. **Keep it alive.** Update and commit the spec when decisions or scope change.

Stop rule: Stops after one phase per run; the next phase starts only after you approve.

## Permissions

- Writes: SPEC.md, SPEC-*.md, tasks/**, src/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`SPEC.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new feature request. Verification: spec check + your approval. Memory: SPEC.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
