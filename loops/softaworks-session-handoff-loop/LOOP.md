---
name: session-handoff
title: Session Handoff skill
repo: softaworks/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/softaworks/session-handoff
---

# Session Handoff skill

Session handoff creates and resumes comprehensive handoff documents so a fresh AI agent can continue work with zero ambiguity, with scaffolding, validation and staleness checks. For anyone running long agent sessions that exhaust context.

- Install the skill: `npx skills add softaworks/agent-toolkit --skill session-handoff`
- Source: https://github.com/softaworks/agent-toolkit/tree/HEAD/dist/plugins/session-handoff/skills/session-handoff
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A session is ending; Context is getting full; You resume earlier work.
Skip it when: The task is a quick one-off; No context needs preserving.

# Make it a habit: Fresh agents resume with full context.

When a session is ending or context is nearly full, your agent runs create_handoff.py to scaffold a handoff, fills the TODO sections, and validates it with validate_handoff.py. The handoff must have no placeholders, no secrets and a quality score of at least 70.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** session ends or fills (event; Claude Code routine; `context near capacity or you request a handoff`)
- **Verification:** validator passes. Hard checks: validate_handoff.py finds no remaining TODO placeholders; the validator detects no secrets; the quality score is at least 70; referenced files exist. On fail: retry, max 1 retries.
- **Memory:** handoff documents at `.claude/handoffs/`. Read first: the most recent handoff, and any predecessor it continues from.

## Steps

1. **Scaffold.** Run python scripts/create_handoff.py with a task slug, using --continues-from to chain to earlier work.
2. **Fill the sections.** Complete the current state, important context, next steps and decisions in the generated file.
3. **Validate.** Run python scripts/validate_handoff.py and fix placeholders, secrets or a low score.
4. **Confirm.** Report the file location, score and the first action item for the next session.
5. **Resume later.** On resume, list handoffs, check staleness, read the document fully and verify context before working.

Stop rule: Stops after one validated handoff per run, with 1 retry.

## Permissions

- Writes: .claude/handoffs/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.claude/handoffs/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: session ends or fills. Verification: validator passes. Memory: .claude/handoffs/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
