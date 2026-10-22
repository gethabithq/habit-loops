---
name: messaging-performance-analyzer
title: Messaging Performance Analyzer skill
repo: sentdm/sent-plugin
license: MIT
url: https://gethabit.dev/skills/sentdm/messaging-performance-analyzer
---

# Messaging Performance Analyzer skill

The messaging performance analyzer skill turns Sent message, activity and webhook data into one diagnosis of delivery failures, funnel drop-offs, read-rate gaps and fallback problems. For teams running SMS, WhatsApp or RCS traffic on Sent.

- Install the skill: `npx skills add sentdm/sent-plugin --skill messaging-performance-analyzer`
- Source: https://github.com/sentdm/sent-plugin/tree/HEAD/claude-plugins/sent/skills/messaging-performance-analyzer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: delivery rate dropped; messages did not arrive; you have an MDR export.
Skip it when: you need 10DLC registration; you write WhatsApp templates.

# Make it a habit: Delivery drops get caught early.

Every morning the agent runs the MDR funnel script on yesterday's Sent export, splits results by channel and direction, and checks webhook health before naming a cause. It ends with one diagnosis and next step, and logs each day's rates as the baseline.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily delivery report (schedule; cron or Claude Code routine; `0 8 * * *`)
- **Verification:** funnel script exit code. Hard checks: python scripts/analyze_mdr_funnel.py path/to/mdr.csv --threshold N exits 0; global totals reconcile with every channel and direction group; no transition is backfilled from a latest-only status. On fail: notify, max 0 retries.
- **Memory:** daily funnel baseline at `loops/message-delivery-funnel-loop/log.md`. Read first: baseline rates per channel and the last diagnosis.

## Steps

1. **Read the baseline.** Load past rates per channel and the last diagnosis from the log.
2. **Pin the cohort.** Fix the time window, profile, template, channel and recipient segment before counting.
3. **Run funnel script.** Run python scripts/analyze_mdr_funnel.py on the export with --threshold and --format json.
4. **Check webhook health.** If callbacks are missing, compare GET /v3/webhooks/{id}/events with the endpoint before blaming delivery.
5. **Split by channel.** Compare SMS, WhatsApp and RCS funnels on their own, with READ counted only as engagement.
6. **Name one diagnosis.** Give one main diagnosis, a confidence level and the next verification step tied to evidence.
7. **Hand off if needed.** Pass compliance, RCS or template causes to sms-10dlc-registration, rcs-agent-onboarding or waba-template-author.
8. **Update the log.** Write the day's rates and diagnosis as the new baseline.

Stop rule: One export per run and one primary diagnosis.

## Permissions

- Writes: loops/message-delivery-funnel-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/message-delivery-funnel-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily delivery report. Verification: funnel script exit code. Memory: loops/message-delivery-funnel-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
