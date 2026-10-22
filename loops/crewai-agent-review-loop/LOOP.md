---
name: design-agent
title: CrewAI design agent skill
repo: crewaiinc/skills
license: MIT
url: https://gethabit.dev/skills/crewaiinc/design-agent
---

# CrewAI design agent skill

The crewai design agent skill helps developers design CrewAI agents: role, goal and backstory, LLM choice, tools, limits, planning, delegation, knowledge sources and guardrails.

- Install the skill: `npx skills add crewaiinc/skills --skill design-agent`
- Source: https://github.com/crewaiinc/skills/tree/HEAD/skills/design-agent
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: creating a new CrewAI agent; an agent loops or hallucinates; deciding how many agents to use.
Skip it when: designing the task itself; not using CrewAI.

# Make it a habit: Every agent passes the checklist.

Runs when agents.yaml or agent code changes. Your agent checks each CrewAI agent against the design checklist: specific role, clear goal, 3-5 tools, tuned max_iter, explicit llm, timeouts and task-level guardrails, and logs gaps.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** agent config changed (event; GitHub Actions or Claude Code routine; `push touches agents.yaml or crew.py`)
- **Verification:** design checklist passes. Hard checks: every agent sets llm explicitly; no agent has more than 5 tools; YAML keys match @agent method names; allow_delegation is off unless needed; knowledge sources have an explicit embedder. On fail: notify, max 1 retries.
- **Memory:** agent review notes at `loops/crewai-agent-review-loop/notes.md`. Read first: checklist gaps found in earlier reviews.

## Steps

1. **Count agents.** Ask whether the work really needs more than one agent.
2. **Check role and goal.** Make roles specific and goals outcome-focused with quality standards.
3. **Check tools.** Confirm data tasks have tools and each agent has at most five.
4. **Check limits.** Tune max_iter and set LLM and tool timeouts instead of relying on max_execution_time.
5. **Check guardrails.** Move guardrails for critical output onto the Task.
6. **Log gaps.** Write each checklist gap and its fix to the notes.

Stop rule: Stops after reviewing 10 agents per run.

## Permissions

- Writes: loops/crewai-agent-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/crewai-agent-review-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: agent config changed. Verification: design checklist passes. Memory: loops/crewai-agent-review-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
