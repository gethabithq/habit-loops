---
name: netlify-forms
title: Netlify Forms skill
repo: netlify/context-and-tools
license: MIT
url: https://gethabit.dev/skills/netlify/netlify-forms
---

# Netlify Forms skill

The netlify forms skill helps an agent add and debug forms on Netlify sites: detection at deploy time, AJAX submission, file uploads, spam filtering and notifications, including forms in Next.js, Nuxt, SvelteKit, Astro and Gatsby.

- Install the skill: `npx skills add netlify/context-and-tools --skill netlify-forms`
- Source: https://github.com/netlify/context-and-tools/tree/HEAD/agent-plugin/skills/netlify-forms
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add a contact or signup form; A framework form never registers; Submissions go missing.
Skip it when: Your site is not on Netlify; You need a full form backend with custom logic.

# Make it a habit: Every form still gets submissions.

When a pull request changes a form, your agent checks unique form names, the public/__forms.html skeleton with matching fields, URL-encoded AJAX bodies and extensionless action paths. A notes file keeps the forms and fields already registered.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** form markup changed (event; GitHub Actions or Claude Code routine; `pull_request touching files with data-netlify forms`)
- **Verification:** skeleton matches every form. Hard checks: each form name is unique per site; every JS-rendered form has a twin in public/__forms.html with the same field names; AJAX posts use URL-encoded bodies, not JSON; no action path ends in .html. On fail: notify, max 0 retries.
- **Memory:** registered forms list at `loops/netlify-forms-check-loop/forms.md`. Read first: form names and fields from the last run.

## Steps

1. **Find the forms.** Your agent lists every form tag with data-netlify or netlify in the changed files.
2. **Check names.** Each form name must be unique and match its hidden form-name input.
3. **Check the skeleton.** JS-rendered and SSR forms need a hidden copy in public/__forms.html with exactly the same fields.
4. **Check submissions.** AJAX code must send URL-encoded bodies, and SSR apps must post to /__forms.html, not /.
5. **Check success pages.** Custom action paths must be extensionless, like /thank-you.
6. **Report and record.** The agent comments the failed checks and updates the list of registered forms.

Stop rule: Stops after one pull request and at most 20 forms per run.

## Permissions

- Writes: loops/netlify-forms-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/netlify-forms-check-loop/forms.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: form markup changed. Verification: skeleton matches every form. Memory: loops/netlify-forms-check-loop/forms.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
