---
name: mempalace-task
title: MemPalace Task skill
repo: mempalace/mempalace
license: MIT
url: https://gethabit.dev/skills/mempalace/mempalace-task
---

# MemPalace Task skill

Mempalace task creates, hands off, claims, executes and closes agent tasks through the MemPalace logstream, with exact branch and base commit and a ready-to-paste handoff. For teams delegating work between coordinated agents.

- Install the skill: `npx skills add mempalace/mempalace --skill mempalace-task`
- Source: https://github.com/mempalace/mempalace/tree/HEAD/.claude-plugin/skills/mempalace-task
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You delegate work to another agent; You prepare a task to hand off; You receive a MemPalace task id.
Skip it when: You work solo in one session; MemPalace is not set up.

# Make it a habit: Tasks handed between agents through logstream.

When you delegate work, your agent verifies the MemPalace coordination seam, normalizes the task with an exact branch and base commit, gets your approval, then creates it with mempalace_task_create and returns the ready-to-paste handoff. Delivery closes back through MemPalace.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you delegate a task (manual; Claude Code routine; `on request`)
- **Verification:** approved + created. Hard checks: mempalace task --help and mempalace_task_create exist; the base commit is an exact hexadecimal id, not a branch or tag; you approved the exact normalized task before it was created; the ready-to-paste handoff line is returned unchanged. On fail: stop, max 0 retries.
- **Memory:** task handoff log at `loops/agent-task-handoff-loop/log.md`. Read first: open tasks, their ids and destination agents.

## Steps

1. **Verify the seam.** Confirm mempalace --version, the task commands and MCP tools, and the current agent identity.
2. **Gather the fields.** Collect project, requester and worker identities, goal, branch, exact base commit and definition of done.
3. **Normalize and approve.** Show you the exact normalized task and get approval, since logstream events are immutable.
4. **Create the task.** Call mempalace_task_create with the approved fields and return the handoff line unchanged.
5. **Execute or close.** A worker claims, does the work, submits a patch or a verbatim reply, and the requester acknowledges applied or failed.

Stop rule: Stops after one task is created or closed per run.

## Permissions

- Writes: loops/agent-task-handoff-loop/**
- Network: none
- Sends: a task to another agent through the MemPalace logstream, after your approval
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agent-task-handoff-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you delegate a task. Verification: approved + created. Memory: loops/agent-task-handoff-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
