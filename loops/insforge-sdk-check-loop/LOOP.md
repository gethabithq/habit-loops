---
name: insforge
title: InsForge skill
repo: InsForge/insforge-skills
license: Apache-2.0
url: https://gethabit.dev/skills/insforge/insforge
---

# InsForge skill

The insforge skill guides your agent through app code with @insforge/sdk: database CRUD, auth, storage, functions, AI through OpenRouter, realtime, email and Stripe or Razorpay payments. For developers building apps on an InsForge backend.

- Install the skill: `npx skills add InsForge/insforge-skills --skill insforge`
- Source: https://github.com/InsForge/insforge-skills/tree/HEAD/skills/insforge
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You add auth or data fetching with InsForge; You upload files to InsForge Storage; You wire checkout or subscriptions in app code.
Skip it when: You need migrations or CLI work, use insforge-cli; Your app does not use InsForge.

# Make it a habit: Catch InsForge SDK mistakes early.

When a pull request changes code that uses @insforge/sdk, your agent checks the key rules: array inserts, bounded reads, no admin key in public env vars, .env files kept local, and a local build. It keeps a list of issues found per module.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches InsForge code (event; GitHub Actions or Claude Code routine; `pull_request touching files that import @insforge/sdk`)
- **Verification:** SDK rule check + build. Hard checks: local build passes; every database insert passes an array; list reads name columns and use .limit(); no API key or OPENROUTER_API_KEY sits in a NEXT_PUBLIC_, VITE_, PUBLIC_ or REACT_APP_ variable; .env, .env.local and .env*.local are listed in .gitignore. On fail: notify, max 1 retries.
- **Memory:** SDK issues list at `loops/insforge-sdk-check-loop/issues.md`. Read first: issues already found per module and which are fixed.

## Steps

1. **Map the change.** List which modules the diff touches: database, auth, storage, functions, AI, realtime, email or payments.
2. **Read the guide.** Open the matching sdk-integration.md or payment guide for each module.
3. **Check keys.** Make sure the anon key is used for user clients and createAdminClient stays in server-only code.
4. **Check data rules.** Look for non-array inserts, unbounded select() polling and storage records missing url or key.
5. **Check backend needs.** If the code needs a new schema, RLS policy or auth change, point to a backend branch with insforge-cli.
6. **Build and report.** Run the local build, post findings and update the issues list.

Stop rule: Stops after one pull request per run and one build retry.

## Permissions

- Writes: loops/insforge-sdk-check-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/insforge-sdk-check-loop/issues.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches InsForge code. Verification: SDK rule check + build. Memory: loops/insforge-sdk-check-loop/issues.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
