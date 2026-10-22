---
name: email-best-practices
title: Email best practices skill
repo: resend/resend-skills
license: MIT
url: https://gethabit.dev/skills/resend/email-best-practices
---

# Email best practices skill

The email best practices skill by Resend guides developers through deliverable, compliant and accessible email: SPF, DKIM and DMARC, transactional versus marketing mail, consent, retries, webhooks, bounce handling and screen reader friendly templates.

- Install the skill: `npx skills add resend/resend-skills --skill email-best-practices`
- Source: https://github.com/resend/resend-skills/tree/HEAD/skills/email-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your emails land in spam; You build signup or transactional emails; You need CAN-SPAM, GDPR or CASL compliance.
Skip it when: Your app sends no email; You need a full email sending SDK guide.

# Make it a habit: Emails stay deliverable and accessible.

Once a week your agent reviews your app's email setup against the email best practices guides: DNS authentication, accessibility of templates, consent and compliance, retries and suppression of bounces. Findings go to a board for the next review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly email review (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** checklist items all pass. Hard checks: SPF, DKIM and DMARC are set for the sending domain; every template sets lang, a <title> and alt text on images; marketing sends have recorded consent and an unsubscribe path; bounced and complained addresses are on the suppression list. On fail: notify, max 0 retries.
- **Memory:** open email issues board at `loops/email-best-practices-loop/board.md`. Read first: open findings from the last review and what was fixed since.

## Steps

1. **Read the board.** Start from the open findings of the last review.
2. **Check deliverability.** Compare the sending domain's SPF, DKIM and DMARC setup with the deliverability guide.
3. **Check accessibility.** Review templates for lang and dir, presentational tables, headings, alt text, title and contrast.
4. **Check compliance.** Confirm marketing mail follows the capture, consent and CAN-SPAM, GDPR and CASL guidance.
5. **Check reliability.** Look for idempotent sends with retry and for webhook events that update the suppression list.
6. **Update the board.** Write each failed item as a task and close the ones that now pass.

Stop rule: One review per run, at most 20 findings written.

## Permissions

- Writes: loops/email-best-practices-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/email-best-practices-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly email review. Verification: checklist items all pass. Memory: loops/email-best-practices-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
