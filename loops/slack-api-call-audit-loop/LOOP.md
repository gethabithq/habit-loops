---
name: slack-api
title: Slack Web API skill
repo: slackapi/slack-skills-plugin
license: MIT
url: https://gethabit.dev/skills/slackapi/slack-api
---

# Slack Web API skill

The slack web api skill helps developers find the right Slack method, read its scopes, token type and arguments from the live docs, call it safely, page with cursors and handle rate limits and errors.

- Install the skill: `npx skills add slackapi/slack-skills-plugin --skill slack-api`
- Source: https://github.com/slackapi/slack-skills-plugin/tree/HEAD/skills/slack-api
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you need the Slack method for a task; a call fails with missing_scope; you must page through results.
Skip it when: you only build Block Kit layouts; you do not use Slack.

# Make it a habit: Slack API calls stay correct.

When code that calls the Slack Web API changes, your agent checks each method against its live doc page: name, scopes, token type, pagination and deprecation. It keeps a log of verified methods so later runs only check what is new.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes Slack calls (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize, files calling slack.com/api`)
- **Verification:** methods match live docs. Hard checks: every method name appears on the live method index; no deprecated method used without its replacement noted; code checks the ok field of every response; pagination uses next_cursor, not page numbers; no bearer token committed in code. On fail: notify, max 0 retries.
- **Memory:** verified method log at `loops/slack-api-call-audit-loop/log.md`. Read first: methods already verified with their scopes and token types.

## Steps

1. **List called methods.** The agent collects every family.method name the changed code calls.
2. **Check the index.** It confirms each name on the live methods.md index at docs.slack.dev.
3. **Read each contract.** For new methods it reads the method page for HTTP verb, scopes, token type, arguments and rate tier.
4. **Review error handling.** It checks that the code reads ok and error, and honors Retry-After on ratelimited.
5. **Review pagination.** Collection calls must loop on response_metadata.next_cursor until it is empty.
6. **Report and log.** Findings go into a review comment and the log; no write method is ever run without the developer saying yes.

Stop rule: Stops after one pull request and at most 30 methods per run.

## Permissions

- Writes: loops/slack-api-call-audit-loop/**
- Network: docs.slack.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/slack-api-call-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes Slack calls. Verification: methods match live docs. Memory: loops/slack-api-call-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
