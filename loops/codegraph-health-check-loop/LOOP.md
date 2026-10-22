---
name: codegraph-ast-grep
title: CodeGraph and ast-grep skill
repo: stark-ai-de/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/stark-ai-de/codegraph-ast-grep
---

# CodeGraph and ast-grep skill

The codegraph and ast-grep skill sets up, updates or diagnoses CodeGraph and the ast-grep CLI so coding agents get semantic repository scope and structural code search, with persisted guidance and safe migrations.

- Install the skill: `npx skills add stark-ai-de/agent-skills --skill codegraph-ast-grep`
- Source: https://github.com/stark-ai-de/agent-skills/tree/HEAD/plugins/stark-ai-developer/skills/codegraph-ast-grep
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: setting up semantic code search; updating CodeGraph or ast-grep; the analysis setup seems broken.
Skip it when: the stack is already ready; you need a dependency audit.

# Make it a habit: Code analysis tools stay ready.

Every week your agent runs the doctor workflow on your CodeGraph and ast-grep setup: versions, config, MCP exposure, guidance and index freshness. It never repairs; it logs the diagnosis and recommends setup or update when needed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly analysis stack check (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** doctor report, you approve. Hard checks: codegraph and ast-grep executables found with versions; MCP tools exposed to the client; repository guidance file present; no install, update or repair ran. On fail: notify, max 0 retries.
- **Memory:** stack health log at `loops/codegraph-health-check-loop/log.md`. Read first: last diagnosis, versions and recommended follow-up.

## Steps

1. **Announce doctor.** The agent states the doctor workflow, the exact root and that nothing will be repaired.
2. **Inspect the setup.** It checks executables, versions, config, MCP registration, CODEGRAPH_DIR state and repository guidance.
3. **Ask before deep checks.** Before codegraph status or a graph query that may migrate metadata, it asks you to approve the exact root.
4. **Gather analytics.** With approval it reports freshness, indexed languages and query readiness; without it, it reports the skipped check.
5. **Log and recommend.** It writes the diagnosis to the log and suggests setup or update as a separate step.

Stop rule: Stops after one doctor pass per run.

## Permissions

- Writes: loops/codegraph-health-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/codegraph-health-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly analysis stack check. Verification: doctor report, you approve. Memory: loops/codegraph-health-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
