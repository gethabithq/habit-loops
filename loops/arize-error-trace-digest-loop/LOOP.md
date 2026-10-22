---
name: arize-trace
title: Arize Trace skill
repo: arize-ai/arize-skills
license: MIT
url: https://gethabit.dev/skills/arize-ai/arize-trace
---

# Arize Trace skill

The arize trace skill downloads and inspects Arize traces, spans and sessions with the ax CLI to see what an LLM app is doing, debug errors and find regressions. For teams running LLM apps instrumented with Arize.

- Install the skill: `npx skills add arize-ai/arize-skills --skill arize-trace`
- Source: https://github.com/arize-ai/arize-skills/tree/HEAD/skills/arize-trace
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: exporting a trace by id; investigating error spans; downloading a conversation session.
Skip it when: you do not use Arize; the app is not instrumented yet.

# Make it a habit: A daily digest of failing traces.

Each day, your agent exports error traces from Arize with the ax CLI for a UTC window, reads the error spans, and writes a digest with span counts and error types. A run log keeps each day's counts and trace ids.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily error digest (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** export counted, not truncated. Hard checks: the export reports a span count; a result equal to the limit is flagged as truncated; the digest file is written. On fail: notify, max 1 retries.
- **Memory:** daily error log at `loops/arize-error-trace-digest-loop/run-log.md`. Read first: yesterday's error counts and trace ids.

## Steps

1. **Set the window.** Your agent gets the current UTC time and sets --start-time at least 12 hours back to cover index lag.
2. **Export errors.** It runs ax traces export with a status_code ERROR filter into .arize-tmp-traces.
3. **Count spans.** It states the span count and flags a result that hits the limit as likely truncated.
4. **Read error spans.** It reads attributes.error.type and attributes.error.message on each error span.
5. **Write digest.** It writes the day's error types and trace ids to the digest and run log.

Stop rule: Stops after one day's export per run, with at most one retry on an auth or project error.

## Permissions

- Writes: .arize-tmp-traces/**, loops/arize-error-trace-digest-loop/**
- Network: api.arize.com, app.arize.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/arize-error-trace-digest-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily error digest. Verification: export counted, not truncated. Memory: loops/arize-error-trace-digest-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
