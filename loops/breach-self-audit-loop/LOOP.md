---
name: what-leaked-about-you
title: What Leaked About You skill
repo: useosint/skills
license: MIT
url: https://gethabit.dev/skills/useosint/what-leaked-about-you
---

# What Leaked About You skill

The what leaked about you skill helps your agent check and interpret data-breach exposure for an email, username or phone with Have I Been Pwned, the Pwned Passwords range API and commercial breach search, without ever using leaked credentials. For self-audits and incident response.

- Install the skill: `npx skills add useosint/skills --skill what-leaked-about-you`
- Source: https://github.com/useosint/skills/tree/HEAD/skills/what-leaked-about-you
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit your own leaked data; You triage a possible account takeover; You want the services an account used.
Skip it when: You want to log in with a leaked password; You have no lawful basis to process someone's breach data.

# Make it a habit: Know when your accounts leak.

Each month your agent checks your own email addresses in Have I Been Pwned, grades each breach, and checks your current passwords through the Pwned Passwords range API without sending them. It compares with last month and lists new breaches and accounts to clean up.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly breach check (schedule; Claude Code routine or cron; `0 9 1 * *`)
- **Verification:** privacy-safe check rules. Hard checks: only the first five hex characters of each SHA-1 hash leave the machine; no password or hash is written to the log; every breach found has a confidence grade; no leaked credential is used to log in anywhere; the report lists breaches new since last month. On fail: stop, max 1 retries.
- **Memory:** breach list, no credentials at `loops/breach-self-audit-loop/breaches.md`. Read first: breaches already known, their grades and usernames found.

## Steps

1. **Check emails.** Look up your own addresses in Have I Been Pwned and note each breach and its data classes.
2. **Grade breaches.** Grade each as confirmed, probable, unconfirmed or rejected, and flag combolists and scrapes.
3. **Map services.** List the services and usernames found; send forgotten handles to hunt-a-handle.
4. **Check passwords.** Hash your current passwords locally and query the range API with the five-character prefix only.
5. **Compare and report.** Show what is new since last month and which passwords and accounts to change.

Stop rule: Stops after your own listed addresses each month, with one retry per lookup.

## Permissions

- Writes: loops/breach-self-audit-loop/**
- Network: haveibeenpwned.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/breach-self-audit-loop/breaches.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly breach check. Verification: privacy-safe check rules. Memory: loops/breach-self-audit-loop/breaches.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
