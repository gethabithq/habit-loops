---
name: adk
title: Botpress ADK skill
repo: botpress/skills
license: MIT
url: https://gethabit.dev/skills/botpress/adk
---

# Botpress ADK skill

The botpress adk skill helps developers build bots with the Botpress Agent Development Kit: actions, tools, workflows, conversations, tables, knowledge bases, triggers, integrations and Zai.

- Install the skill: `npx skills add botpress/skills --skill adk`
- Source: https://github.com/botpress/skills/tree/HEAD/skills/adk
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a Botpress ADK feature; You ask how an ADK primitive works; Your ADK bot shows errors.
Skip it when: You use Botpress Studio only; You do not use TypeScript.

# Make it a habit: ADK bot checked before every session.

At the start of each session on an ADK project, your agent runs adk check and adk status with JSON output plus tsc --noEmit, and raises unconfigured integrations, missing models or type errors before anything else. A log keeps issues found.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** ADK session starts (event; Claude Code routine; `a session opens in a project with agent.config.ts`)
- **Verification:** check, status, typecheck pass. Hard checks: adk check --format json reports no errors; tsc --noEmit passes; imports come from @botpress/runtime, not zod or @botpress/sdk. On fail: notify, max 0 retries.
- **Memory:** health issues log at `loops/botpress-adk-health-loop/run-log.md`. Read first: issues found last session and whether they were fixed.

## Steps

1. **Run checks.** Run adk check --format json and adk status --format json.
2. **Typecheck.** Run tsc --noEmit, since adk check does not typecheck.
3. **Scan patterns.** Check imports, Action handlers and conversation.send use against the critical patterns.
4. **Raise issues.** Mention any problem before the session's task, once per session.
5. **Log.** Record issues and fixes.

Stop rule: Stops after one health check per session.

## Permissions

- Writes: loops/botpress-adk-health-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/botpress-adk-health-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: ADK session starts. Verification: check, status, typecheck pass. Memory: loops/botpress-adk-health-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
