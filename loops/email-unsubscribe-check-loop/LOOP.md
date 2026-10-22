---
name: extension-email-marketing
title: Extension Email Marketing skill
repo: caffeinelabs/skills
license: Apache-2.0
url: https://gethabit.dev/skills/caffeinelabs/extension-email-marketing
---

# Extension Email Marketing skill

The extension email marketing skill helps Caffeine AI app builders add marketing email to subscribers, with topics, email verification and a working unsubscribe page.

- Install the skill: `npx skills add caffeinelabs/skills --skill extension-email-marketing`
- Source: https://github.com/caffeinelabs/skills/tree/HEAD/skills/extension-email-marketing
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build a Caffeine app that sends newsletters; You need topic-based subscriber lists; You upgrade from an older email-marketing version.
Skip it when: Your app is not built on Caffeine AI; You only send transactional mail.

# Make it a habit: Every marketing mail can unsubscribe.

When backend or frontend code changes in a Caffeine app with marketing email, your agent walks the six setup steps of the skill, checks the unsubscribe placeholder and the public /unsubscribe route, and logs what it found for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** email code changed (event; GitHub Actions or Claude Code routine; `push touching src/backend/main.mo or src/frontend/**`)
- **Verification:** six setup steps present. Hard checks: mops dependencies caffeineai-email-marketing, caffeineai-email-verification and caffeineai-authorization are added; main.mo includes MixinEmailUnsubscribe(emailSubscribers, unsubscribeTokens) and MixinEmailVerification; a public /unsubscribe route exists outside any signed-in layout; confirm() is called only from a button click, never on page load; app code does not call EmailClient.broadcast; build passes. On fail: notify, max 1 retries.
- **Memory:** setup check log at `loops/email-unsubscribe-check-loop/run-log.md`. Read first: setup steps that failed last run.

## Steps

1. **Read the log.** The agent reads which setup steps failed in the last run.
2. **Check dependencies.** It confirms the mops packages and the @caffeineai/email-marketing npm package are installed.
3. **Check backend state.** It looks for the stable fields emailSubscribers and unsubscribeTokens plus the verification states in the migration chain head.
4. **Check sending.** It confirms mail goes through EmailMarketing.sendMarketingEmail or sendMarketingEmailTo and the body carries {{UNSUBSCRIBE_URL}}.
5. **Check unsubscribe page.** It confirms the /unsubscribe route is public and uses the useUnsubscribe hook with a button.
6. **Check verification skill.** It also runs the checks of extension-email-verification, which this skill depends on.
7. **Log and report.** It writes each step as pass or fail to the run log and notifies you on a fail.

Stop rule: Stops after one pass over the six setup steps per run, with at most one retry.

## Permissions

- Writes: loops/email-unsubscribe-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/email-unsubscribe-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: email code changed. Verification: six setup steps present. Memory: loops/email-unsubscribe-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
