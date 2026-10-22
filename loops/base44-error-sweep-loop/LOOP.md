---
name: base44-troubleshooter
title: Base44 Troubleshooter skill
repo: base44/skills
license: MIT
url: https://gethabit.dev/skills/base44/base44-troubleshooter
---

# Base44 Troubleshooter skill

The base44 troubleshooter skill helps an agent debug production issues in Base44 apps using function logs and workflow run history: failed runs, error logs, and why a scheduled job stopped firing. For developers running Base44 apps.

- Install the skill: `npx skills add base44/skills --skill base44-troubleshooter`
- Source: https://github.com/base44/skills/tree/HEAD/skills/base44-troubleshooter
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You investigate a Base44 app error; A scheduled job or automation failed; You debug a function call.
Skip it when: You build a new Base44 app; The app is not on Base44.

# Make it a habit: Catch Base44 failures each morning.

Each morning the agent confirms it is signed in, lists failed workflow runs and pulls error-level function logs for your Base44 app. It reads the failing task and error, correlates timestamps and keeps a log so the next run sees what is new.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine or cron; `0 8 * * *`)
- **Verification:** auth and log checks. Hard checks: base44 whoami confirms a signed-in session; base44 workflows runs --status failed exits zero; base44 logs --level error returns without an auth error. On fail: notify, max 1 retries.
- **Memory:** incident log at `loops/base44-error-sweep-loop/log.md`. Read first: failed runs and errors already seen and their resolution.

## Steps

1. **Check auth.** Run base44 whoami and tell the user to log in if the token expired.
2. **List failed runs.** Run base44 workflows runs --status failed and read each failing task and error.
3. **Check workflows.** Run base44 workflows list and flag any with consecutiveFailures above zero.
4. **Pull errors.** Run base44 logs --level error, and re-run after a wait when a result is empty, since logs lag.
5. **Correlate.** Match error timestamps and the failing task to the function that failed.
6. **Log the sweep.** Write new failures and their likely cause to the log.

Stop rule: Stops after one sweep of failed runs and error logs per run.

## Permissions

- Writes: loops/base44-error-sweep-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/base44-error-sweep-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: auth and log checks. Memory: loops/base44-error-sweep-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
