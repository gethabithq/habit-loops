---
name: openai-agents-sdk
title: OpenAI Agents SDK skill
repo: laguagu/claude-code-nextjs-skills
license: MIT
url: https://gethabit.dev/skills/laguagu/openai-agents-sdk
---

# OpenAI Agents SDK skill

The openai agents sdk skill helps Python developers build agents with the openai-agents package: tools, handoffs, guardrails, sessions, streaming, tracing and offline testing.

- Install the skill: `npx skills add laguagu/claude-code-nextjs-skills --skill openai-agents-sdk`
- Source: https://github.com/laguagu/claude-code-nextjs-skills/tree/HEAD/skills/openai-agents-sdk
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build agents in Python; You add function tools or handoffs; You test agent flows offline.
Skip it when: You use the TypeScript SDK; You do not use openai-agents.

# Make it a habit: Agent changes verified offline first.

On every pull request that touches agents code, your agent reads the installed openai-agents version, checks tools, history and approval paths, and runs offline orchestration tests with ScriptedModel and tracing disabled. A log keeps the SDK version and results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** agents code changes (event; GitHub Actions or Claude Code routine; `pull_request touches files importing agents`)
- **Verification:** offline tests pass. Hard checks: ScriptedModel tests pass with model.assert_complete(); no Runner.run_sync inside a running event loop; every tool with side effects checks authorization; project checks pass. On fail: notify, max 1 retries.
- **Memory:** sdk test log at `loops/openai-agents-test-loop/run-log.md`. Read first: installed SDK version and last failures.

## Steps

1. **Read the version.** Get the version with importlib.metadata and check exports in agents/__init__.py.
2. **Read references.** Read the reference for the changed feature, such as references/tools.md or references/sessions.md.
3. **Check patterns.** Confirm await Runner.run in async code and handoffs versus as_tool choices.
4. **Test offline.** Run ScriptedModel tests with RunConfig(tracing_disabled=True).
5. **Run checks.** Run the project's checks and report missing provider access separately.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/openai-agents-test-loop/**
- Network: openai.github.io, developers.openai.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/openai-agents-test-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: agents code changes. Verification: offline tests pass. Memory: loops/openai-agents-test-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
