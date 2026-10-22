---
name: waba-template-author
title: WABA Template Author skill
repo: sentdm/sent-plugin
license: MIT
url: https://gethabit.dev/skills/sentdm/waba-template-author
---

# WABA Template Author skill

The waba template author skill writes, classifies, validates and repairs WhatsApp templates as Sent v3 template requests, with variables, buttons, authentication settings and a linter. For teams sending WhatsApp messages through Sent.

- Install the skill: `npx skills add sentdm/sent-plugin --skill waba-template-author`
- Source: https://github.com/sentdm/sent-plugin/tree/HEAD/claude-plugins/sent/skills/waba-template-author
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you write a new WhatsApp template; Meta rejected a template; you build an OTP template.
Skip it when: you design a template editor UI; you need to connect a WABA.

# Make it a habit: WhatsApp templates pass review first time.

When a new WhatsApp message is needed or a template comes back rejected, the agent picks the category, builds the Sent v3 request, defines variables and buttons, and runs the template linter. It asks you before submitting for review and logs each template's status.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** template needed or rejected (event; Claude Code routine; `new template request or webhook payload.status == REJECTED`)
- **Verification:** linter + your OK. Hard checks: python scripts/lint_waba_template.py template.json passes; every placeholder has one matching variable with props.sample; body stays at or below 1,024 characters; button counts stay within the per-type limits. On fail: retry, max 2 retries.
- **Memory:** template status log at `loops/whatsapp-template-lint-loop/log.md`. Read first: templates already drafted, their category and last known status.

## Steps

1. **Set intent and category.** Collect the business event and language, then choose UTILITY, MARKETING or AUTHENTICATION.
2. **Build the request.** Write the POST /v3/templates body with definition, category, language and sandbox true.
3. **Define variables.** Give each placeholder a unique id, a name, a matching type and a realistic sample.
4. **Add buttons.** Add only supported button types within the total and per-type limits.
5. **Run the linter.** Run python scripts/lint_waba_template.py template.json and fix every error it reports.
6. **Ask before submitting.** Show you the final payload and explain that submit_for_review changes external state.
7. **Track the status.** Store the raw payload.status from template webhooks and log the result.

Stop rule: One template per run, at most 2 lint-and-fix retries.

## Permissions

- Writes: template.json, loops/whatsapp-template-lint-loop/
- Network: none
- Sends: template submission for provider review
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/whatsapp-template-lint-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: template needed or rejected. Verification: linter + your OK. Memory: loops/whatsapp-template-lint-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
