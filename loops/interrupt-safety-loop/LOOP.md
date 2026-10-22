---
name: langgraph-human-in-the-loop
title: LangGraph Human in the Loop skill
repo: langchain-ai/langchain-skills
license: MIT
url: https://gethabit.dev/skills/langchain-ai/langgraph-human-in-the-loop
---

# LangGraph Human in the Loop skill

The langgraph human in the loop skill shows developers how to pause a LangGraph graph with interrupt(), resume it with Command(resume=...), build approval and validation flows, and keep side effects safe on resume.

- Install the skill: `npx skills add langchain-ai/langchain-skills --skill langgraph-human-in-the-loop`
- Source: https://github.com/langchain-ai/langchain-skills/tree/HEAD/config/skills/langgraph-human-in-the-loop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Adding an approval step to a graph; Validating human input in a loop; Resuming parallel interrupts.
Skip it when: Graphs with no human step; Projects without LangGraph.

# Make it a habit: Paused graphs resume without duplicates.

On each pull request that touches LangGraph nodes, the agent checks that graphs with interrupt() compile with a checkpointer, resume through Command(resume=...) on the same thread_id and keep side effects before interrupt() idempotent. Tests must pass.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches graph code (event; GitHub Actions; `pull_request opened or synchronize`)
- **Verification:** interrupt rules + tests. Hard checks: every graph that calls interrupt() compiles with a checkpointer; resume uses Command(resume=...), never Command(update=...) as invoke input; no insert or list append runs before interrupt(); tests pass. On fail: notify, max 1 retries.
- **Memory:** flagged nodes log at `loops/interrupt-safety-loop/runs.md`. Read first: nodes flagged before and whether they were fixed.

## Steps

1. **Find interrupts.** The agent lists every node that calls interrupt().
2. **Check checkpointer.** Each such graph must compile with InMemorySaver or PostgresSaver.
3. **Check resume.** Resume must use Command(resume=...) with the same thread_id.
4. **Check payloads.** Values passed to interrupt() must be JSON-serializable.
5. **Check side effects.** Code before interrupt() must use upsert or check-before-create, or move after it.
6. **Run tests.** It runs the tests and logs any node that fails a check.

Stop rule: Stops after one pull request and at most 10 graph files per run.

## Permissions

- Writes: loops/interrupt-safety-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/interrupt-safety-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches graph code. Verification: interrupt rules + tests. Memory: loops/interrupt-safety-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
