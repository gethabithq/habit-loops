---
name: langchain-fundamentals
title: LangChain Fundamentals skill
repo: langchain-ai/langchain-skills
license: MIT
url: https://gethabit.dev/skills/langchain-ai/langchain-fundamentals
---

# LangChain Fundamentals skill

The langchain fundamentals skill shows developers how to build LangChain agents with create_agent, define tools with @tool or tool(), add middleware for human approval and error handling, and get structured output.

- Install the skill: `npx skills add langchain-ai/langchain-skills --skill langchain-fundamentals`
- Source: https://github.com/langchain-ai/langchain-skills/tree/HEAD/config/skills/langchain-fundamentals
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Building a new LangChain agent; Defining tools for an agent; Adding approval middleware.
Skip it when: You use another agent framework; You only need a single model call.

# Make it a habit: LangChain agents built the current way.

On each pull request that touches agent code, the agent checks that agents use create_agent, tools carry clear descriptions, memory has a checkpointer and thread_id, and invoke calls set recursion_limit. Tests must pass; findings go to a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches agent code (event; GitHub Actions; `pull_request opened or synchronize`)
- **Verification:** pattern check + tests. Hard checks: every agent is built with create_agent(); every tool has a docstring or description with Args; every invoke call sets recursion_limit; tests pass. On fail: notify, max 1 retries.
- **Memory:** agent review log at `loops/agent-build-check-loop/runs.md`. Read first: files and patterns flagged in earlier reviews.

## Steps

1. **Find agents.** The agent lists the agent and tool definitions in the change.
2. **Check construction.** Agents must use create_agent(), with middleware for custom flows.
3. **Check tools.** Each @tool or tool() needs a specific description and its Args.
4. **Check memory.** Agents that must remember need a checkpointer such as MemorySaver and a thread_id.
5. **Check limits.** invoke calls need recursion_limit so a run cannot loop forever.
6. **Check results.** Code reads the last entry of result messages, not result.content.
7. **Run tests.** It runs the test suite and logs the findings.

Stop rule: Stops after one pull request and at most 10 agent files per run.

## Permissions

- Writes: loops/agent-build-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agent-build-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches agent code. Verification: pattern check + tests. Memory: loops/agent-build-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
