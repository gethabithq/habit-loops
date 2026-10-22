---
name: vibe-security
title: Vibe Security skill
repo: raroque/vibe-security-skill
license: MIT
url: https://gethabit.dev/skills/raroque/vibe-security
---

# Vibe Security skill

Vibe Security audits codebases for the security holes AI assistants commonly introduce: exposed secrets, broken access control, missing auth, client-trust and payment flaws. For developers shipping AI-built apps.

- Install the skill: `npx skills add raroque/vibe-security-skill --skill vibe-security`
- Source: https://github.com/raroque/vibe-security-skill/tree/HEAD/vibe-security
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: auditing an AI-built app for security; checking secrets, auth or database rules; reviewing payment and access control flows.
Skip it when: you want a non-security code review; the project handles no secrets, auth or user data.

# Make it a habit: Common AI-coded security holes caught.

When code changes, your agent audits it for the holes AI code tends to introduce: exposed secrets, weak database access rules, missing auth, client-trust and payment flaws, and reports findings by severity with before-and-after fixes. A run log keeps prior findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** code changes (event; GitHub Actions or Claude Code routine; `push or pull request`)
- **Verification:** findings by severity. Hard checks: secrets scan finds no hardcoded keys or client-exposed secret prefixes; .env is in .gitignore; database access rules exist where the stack uses them; findings are ordered Critical to Low with file and line. On fail: notify, max 1 retries.
- **Memory:** security findings log at `loops/vibe-security-audit-loop/run-log.md`. Read first: prior findings and which areas were already clean.

## Steps

1. **Scan secrets.** Your agent scans for hardcoded keys, client-exposed secret prefixes and a missing .gitignore entry.
2. **Check database access.** It checks Supabase RLS, Firebase rules or Convex auth guards where the stack uses them.
3. **Check auth.** It validates token handling, middleware auth and server action protection.
4. **Check payments and limits.** It checks for client-side price trust, webhook signature checks and rate limits on costly operations.
5. **Report.** It orders findings Critical to Low with file and line, impact and a before-and-after fix.

Stop rule: Stops after one audit per run, with at most one re-scan.

## Permissions

- Writes: loops/vibe-security-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/vibe-security-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: code changes. Verification: findings by severity. Memory: loops/vibe-security-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
