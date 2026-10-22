---
name: resend-cli
title: Resend CLI skill
repo: resend/resend-skills
license: MIT
url: https://gethabit.dev/skills/resend/resend-cli
---

# Resend CLI skill

The resend cli skill teaches agents to run the resend command line tool safely in scripts and CI: sending email and React Email templates, managing domains, contacts, broadcasts, webhooks, inboxes and logs, with the non-interactive flag rules that avoid silent failures.

- Install the skill: `npx skills add resend/resend-skills --skill resend-cli`
- Source: https://github.com/resend/resend-skills/tree/HEAD/skills/resend-cli
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You run Resend from scripts or CI; Your agent sends or previews email in the shell; You manage domains or webhooks from the terminal.
Skip it when: You call Resend only through an SDK; You do not use Resend.

# Make it a habit: Catch Resend setup problems early.

Every morning your agent runs read-only resend CLI commands in quiet JSON mode: doctor, domain status, recent request logs and usage. Exit codes and JSON fields decide pass or fail, and a run log keeps what changed since yesterday.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily Resend check (schedule; GitHub Actions or cron; `0 7 * * *`)
- **Verification:** CLI exit codes clean. Hard checks: resend doctor -q exits 0; domains get shows each domain verified; logs list shows no new error entries since last run; no error JSON on stderr. On fail: notify, max 1 retries.
- **Memory:** daily Resend check log at `loops/resend-cli-loop/runs.md`. Read first: last run's domain status, usage and error log ids.

## Steps

1. **Check the CLI.** Run resend --version and stop if the CLI is missing or RESEND_API_KEY is not set.
2. **Run doctor.** Call resend doctor -q and record the exit code.
3. **Check domains.** List domains, then use domains get <id> on each to read its status and records.
4. **Scan request logs.** Run logs list and open new failures with logs get <id> for the bodies.
5. **Read usage.** Run resend usage and compare quota use with the last run.
6. **Log and notify.** Write the results to the run log and flag every failed check.

Stop rule: One pass per run, at most 20 log entries opened.

## Permissions

- Writes: loops/resend-cli-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/resend-cli-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily Resend check. Verification: CLI exit codes clean. Memory: loops/resend-cli-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
