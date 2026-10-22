---
name: auth0
title: Auth0 skill
repo: auth0/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/auth0/auth0
---

# Auth0 skill

Auth0 skill helps agents add and fix authentication with Auth0: login, sessions, route guards, MFA, passkeys, SSO, Organizations, branding, tenant audits and provider migrations, across every major framework and SDK. For developers securing apps and APIs.

- Install the skill: `npx skills add auth0/agent-skills --skill auth0`
- Source: https://github.com/auth0/agent-skills/tree/HEAD/plugins/auth0/skills/auth0
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You add login to an app; You debug a 401 or callback error; You audit an Auth0 tenant.
Skip it when: You use another identity provider only; You need no user authentication.

# Make it a habit: Tenant security issues found monthly.

Once a month your agent runs the Auth0 audit intent: it loads the audit, remediation and tooling references, scans the tenant with CheckMate and reports findings. Fixes run only with your per-command confirmation, and each change is verified by re-fetch.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly tenant audit (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** re-fetch check + approval. Hard checks: each applied fix is confirmed by re-fetching the setting; the findings report exists; no fix runs without a per-command confirmation. On fail: notify, max 0 retries.
- **Memory:** audit findings log at `loops/auth0-tenant-audit-loop/log.md`. Read first: open findings and fixes already applied.

## Steps

1. **Detect intent.** Use the audit intent, or healthcheck when you want scores and a plan recommendation.
2. **Detect tooling.** Pick terraform, MCP, Vercel or the default CLI tooling reference from the project tree.
3. **Load references.** Read the feature-audit, feature-audit-pricing, feature-audit-remediation and tooling index files.
4. **Scan the tenant.** Run the audit workflow and write a findings report.
5. **Confirm fixes.** Ask you before each remediation command and skip any you decline.
6. **Verify by re-fetch.** Re-fetch every changed setting to confirm the fix landed and log it.

Stop rule: Stops after one tenant audit and at most 10 fixes per run.

## Permissions

- Writes: loops/auth0-tenant-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/auth0-tenant-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly tenant audit. Verification: re-fetch check + approval. Memory: loops/auth0-tenant-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
