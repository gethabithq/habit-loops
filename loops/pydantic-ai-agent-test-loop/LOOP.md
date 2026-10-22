---
name: building-pydantic-ai-agents
title: Building Pydantic AI Agents skill
repo: pydantic/skills
license: MIT
url: https://gethabit.dev/skills/pydantic/building-pydantic-ai-agents
---

# Building Pydantic AI Agents skill

The building pydantic ai agents skill gives patterns for Python agents with Pydantic AI: tools, capabilities and on-demand loading, structured output, streaming, hooks, YAML specs, realtime sessions, testing with TestModel and Logfire tracing. For Python developers building agents.

- Install the skill: `npx skills add pydantic/skills --skill building-pydantic-ai-agents`
- Source: https://github.com/pydantic/skills/tree/HEAD/plugins/ai/skills/building-pydantic-ai-agents
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build an agent with Pydantic AI; You add tools or capabilities; You test agent behavior.
Skip it when: You only use pydantic validation; You use LangChain or CrewAI.

# Make it a habit: Keep Pydantic AI agents tested, traced.

When agent code changes, your agent checks the common Pydantic AI gotchas, makes sure each Agent has a name, Caching and Logfire setup, considers defer_loading for capabilities, and runs TestModel tests through agent.override. A log keeps failures.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** agent code changes (event; GitHub Actions or Claude Code routine; `pull request touches files importing pydantic_ai`)
- **Verification:** TestModel tests pass. Hard checks: pytest passes with TestModel via agent.override; model strings include a provider prefix; @agent.tool functions take RunContext first and tool_plain ones do not; no history_processors kwarg in new code. On fail: retry, max 2 retries.
- **Memory:** agent test log at `loops/pydantic-ai-agent-test-loop/runs.md`. Read first: gotchas found before and failing tests.

## Steps

1. **Route the task.** Your agent picks the one reference that fits, such as Agents Core or Tools Core.
2. **Check setup.** It checks each Agent has name=, Caching() and logfire.configure() unless you use another backend.
3. **Check loading.** It considers defer_loading=True for capabilities not needed on most turns.
4. **Check gotchas.** It checks tool decorators, provider prefixes, output_type unions and hook names.
5. **Test.** It runs TestModel or FunctionModel tests inside agent.override.
6. **Log.** It records failures and fixes.

Stop rule: Stops after one change and 2 test fix rounds per run.

## Permissions

- Writes: src/**, tests/**, loops/pydantic-ai-agent-test-loop/**
- Network: pydantic.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pydantic-ai-agent-test-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: agent code changes. Verification: TestModel tests pass. Memory: loops/pydantic-ai-agent-test-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
