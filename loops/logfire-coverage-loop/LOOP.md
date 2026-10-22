---
name: logfire-instrumentation
title: Logfire Instrumentation skill
repo: pydantic/skills
license: MIT
url: https://gethabit.dev/skills/pydantic/logfire-instrumentation
---

# Logfire Instrumentation skill

The logfire instrumentation skill helps developers add Pydantic Logfire traces, logs, metrics and AI agent spans to Python, JavaScript and Rust apps, and verify real data arrived.

- Install the skill: `npx skills add pydantic/skills --skill logfire-instrumentation`
- Source: https://github.com/pydantic/skills/tree/HEAD/plugins/logfire/skills/logfire-instrumentation
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add tracing to an app; You instrument an AI agent framework; Traces are not showing up.
Skip it when: You only monitor hosts or containers; You evaluate agents against test datasets.

# Make it a habit: One more service sending real traces.

Each run your agent confirms the Logfire project with whoami, instruments one service with configure before instrument calls, sets service metadata, triggers a real request and queries Logfire to prove fresh data arrived. A board tracks services left.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** next service to instrument (manual; Claude Code routine; `run when you pick the next service from the board`)
- **Verification:** fresh data queried in Logfire. Hard checks: whoami reports the intended project; projects status --json shows fresh data for the service; service.name is not unknown_service; no LOGFIRE_TOKEN or write token appears in client-side code. On fail: retry, max 2 retries.
- **Memory:** services to instrument at `loops/logfire-coverage-loop/board.md`. Read first: services already verified and the next one to do.

## Steps

1. **Authenticate.** Run the target-aware whoami check first; browser sign-in may need you.
2. **Detect stack.** Read pyproject.toml, package.json or Cargo.toml and pick one representative service.
3. **Instrument.** Install logfire with the matching extras and call configure() before any instrument_*() call.
4. **Set metadata.** Set service.name, service.version and deployment.environment.name.
5. **Verify.** Run a real request and query projects status --json for fresh data, then audit nesting and names.
6. **Report and ask.** Report the project URL and real values, then ask whether to do the next service.

Stop rule: Stops after one verified service per run, with at most 2 fix rounds.

## Permissions

- Writes: pyproject.toml, package.json, Cargo.toml, loops/logfire-coverage-loop/**
- Network: pydantic.dev, registry.npmjs.org
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/logfire-coverage-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: next service to instrument. Verification: fresh data queried in Logfire. Memory: loops/logfire-coverage-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
