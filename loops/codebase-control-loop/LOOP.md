---
name: design-control-loop
title: Design Control Loop skill
repo: humanlayer/skills
license: MIT
url: https://gethabit.dev/skills/humanlayer/design-control-loop
---

# Design Control Loop skill

Design control loop is a skill for engineering teams that interviews you to design an agentic control loop for your codebase, with sensor, controller and actuator, then builds it as local scripts plus a scheduled agent workflow.

- Install the skill: `npx skills add humanlayer/skills --skill design-control-loop`
- Source: https://github.com/humanlayer/skills/tree/HEAD/plugins/design-control-loop/skills/design-control-loop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want steady small PRs toward a goal; You migrate a pattern over time; You raise coverage step by step.
Skip it when: You need a one-off change; Your team cannot review regular PRs.

# Make it a habit: A scheduled loop driving your codebase.

Your agent reads the repo, interviews you to design a set point, sensor, controller and actuator, builds each as a locally runnable piece, then wires them into a scheduled CI workflow that opens one reviewable PR at a time with a memory file for feedback.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you want a loop (manual; Claude Code, then GitHub Actions; `manual: design a control loop`)
- **Verification:** runs locally, YAML parses. Hard checks: sensor, controller and actuator each run locally on their own; the workflow YAML parses; every path named by the skill, workflow and memory file exists; scheduled runs no-op when an open loop PR exists. On fail: retry, max 2 retries.
- **Memory:** loop memory file at `.github/agent-memory/<task-slug>.md`. Read first: standing feedback, scope exclusions and false-positive areas.

## Steps

1. **Understand the repo.** Read CI, package files, validation scripts and existing skills before asking.
2. **Design with the user.** Interview the user on set point, sensor, controller, actuator and disturbances, and write the design down.
3. **Build the actuator skill.** Write .claude/skills/<skill-name>/SKILL.md with golden patterns and a response template.
4. **Run locally.** Land sensor and controller as scripts and run all three pieces by hand.
5. **Wire into CI.** Build the workflow from references/workflow-template.yml as sensor, controller, actuator steps.
6. **Put a human on it.** Add the memory file and optional /iterate support with references/agent-iteration.ts.
7. **Bound and dry-run.** Limit to one open PR per loop, validate the YAML and dry-run with a temporary push trigger.

Stop rule: Stops after one loop design and one dry-run PR per run.

## Permissions

- Writes: .github/workflows/**, .github/agent-memory/**, .claude/skills/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.github/agent-memory/<task-slug>.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you want a loop. Verification: runs locally, YAML parses. Memory: .github/agent-memory/<task-slug>.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
