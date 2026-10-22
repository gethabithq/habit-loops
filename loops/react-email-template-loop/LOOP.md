---
name: react-email
title: React Email skill
repo: resend/resend-skills
license: MIT
url: https://gethabit.dev/skills/resend/react-email
---

# React Email skill

The react email skill builds HTML email templates with React components, renders them to HTML and plain text, embeds the visual email editor and sends with Resend. For developers who write transactional emails and newsletters.

- Install the skill: `npx skills add resend/resend-skills --skill react-email`
- Source: https://github.com/resend/resend-skills/tree/HEAD/skills/react-email
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build transactional email templates; You add an email editor to an app; You render React emails to HTML.
Skip it when: You only send plain text emails; You do not use React.

# Make it a habit: Email templates render in every inbox.

When a pull request changes files in the emails folder, your agent reviews each template with react email, fixes classes that inboxes do not support and exports it to HTML. Hard checks test size and markup, and a log keeps what was fixed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** emails folder changes (event; GitHub Actions or Claude Code routine; `pull_request paths: emails/**`)
- **Verification:** export and markup checks. Hard checks: email export finishes without errors; each exported HTML file stays under 102KB; every Button has box-border and every border has a type; no dark:, sm: or md: classes and no SVG or WEBP images; every Img has an alt attribute. On fail: retry, max 2 retries.
- **Memory:** template fix log at `loops/react-email-template-loop/run-log.md`. Read first: templates fixed before and checks that failed.

## Steps

1. **Find changed templates.** The run lists the templates in the emails folder that the pull request touched.
2. **Ask what is missing.** For a new template without brand color, logo, tone or production URL, the agent asks you first.
3. **Review the markup.** The agent checks structure: Head inside Tailwind, Preview first in Body, one Container, Row and Column instead of flexbox or grid.
4. **Fix the styles.** The agent uses pixelBasedPreset, adds box-border and border types, and removes media query and theme classes.
5. **Check accessibility.** The agent makes sure there is one h1, alt text on images and link text that names the destination.
6. **Export to HTML.** The agent runs email export with --plainText and checks the size of each file.
7. **Log the run.** The run writes each template and its fixes into the run log.

Stop rule: Stops after 10 templates or 2 retries per template.

## Permissions

- Writes: emails/**, loops/react-email-template-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-email-template-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: emails folder changes. Verification: export and markup checks. Memory: loops/react-email-template-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
