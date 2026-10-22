---
name: n8n-credentials-and-security-official
title: n8n Credentials and Security skill
repo: n8n-io/skills
license: Apache-2.0
url: https://gethabit.dev/skills/n8n-io/n8n-credentials-and-security-official
---

# n8n Credentials and Security skill

The n8n credentials and security skill helps builders keep API keys, tokens and OAuth secrets in the n8n credential system, bound by ID, never in text fields or code.

- Install the skill: `npx skills add n8n-io/skills --skill n8n-credentials-and-security-official`
- Source: https://github.com/n8n-io/skills/tree/HEAD/skills/n8n-credentials-and-security-official
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You add auth to an n8n node; Someone pasted a token into chat; No native node exists for a service.
Skip it when: You do not use n8n; You need to create credentials programmatically.

# Make it a habit: No secrets hardcoded in workflows.

Each week your agent scans n8n workflows for tokens in header fields, Set nodes or $vars, lists matching credentials with list_credentials, binds them by ID with setNodeCredential, asks you when several match, and names the exact credential type to create.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly secret scan (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** no plain-text secrets left. Hard checks: no Authorization header value holds a literal token; no Set node or $vars entry holds a secret; every auth node is bound to a credential by ID. On fail: notify, max 0 retries.
- **Memory:** secret audit log at `loops/n8n-secret-audit-loop/run-log.md`. Read first: nodes rebound and credentials you still must create.

## Steps

1. **Scan workflows.** Find secrets in header fields, Set nodes, $vars or SDK code.
2. **List credentials.** Call list_credentials with the type before binding any node.
3. **Bind by ID.** Bind one match with setNodeCredential; ask you when several match.
4. **Name missing types.** Tell you the exact credential type to create in the UI.
5. **Flag leaks.** Mark any secret seen in plain text as leaked and ask you to rotate it.

Stop rule: Stops after 10 workflows per run.

## Permissions

- Writes: loops/n8n-secret-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/n8n-secret-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly secret scan. Verification: no plain-text secrets left. Memory: loops/n8n-secret-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
