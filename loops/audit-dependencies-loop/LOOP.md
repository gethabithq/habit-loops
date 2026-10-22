---
name: audit-dependencies
title: Audit Dependencies skill
repo: payloadcms/payload
license: MIT
url: https://gethabit.dev/skills/payloadcms/audit-dependencies
---

# Audit Dependencies skill

The audit dependencies skill helps pnpm monorepo maintainers fix vulnerabilities from pnpm audit the simplest way: direct bump, lockfile update, or a justified override, then a PR with advisory links.

- Install the skill: `npx skills add payloadcms/payload --skill audit-dependencies`
- Source: https://github.com/payloadcms/payload/tree/HEAD/.agents/skills/audit-dependencies
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: pnpm audit reports vulnerabilities; The audit CI check fails; You need to justify a pnpm override.
Skip it when: You use npm or yarn; You want automatic merges.

# Make it a habit: Vulnerable dependencies fixed the simplest way.

Each week or when the audit check fails, your agent runs the audit script, traces each vulnerable package, picks direct bump, lockfile update or override, shows you the plan, then installs, re-audits, builds and opens a PR with advisory links.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** audit check fails (event; GitHub Actions or Claude Code routine; `audit-dependencies CI check fails, or weekly schedule`)
- **Verification:** you approve, audit exits 0. Hard checks: ./.github/workflows/audit-dependencies.sh exits 0 after fixes; pnpm run build:core passes; every override uses a ^ range and has a justification; each fixed vulnerability has a GHSA link in the PR. On fail: stop, max 0 retries.
- **Memory:** fix(deps) commits at `loops/audit-dependencies-loop/run-log.md`. Read first: earlier overrides and why they were needed.

## Steps

1. **Run the audit.** Run ./.github/workflows/audit-dependencies.sh with the severity, default high.
2. **Trace chains.** Mark each package direct or transitive and walk up to the nearest one you control.
3. **Pick a fix.** Prefer a direct bump, then pnpm update --recursive, then a scoped pnpm override.
4. **Show the plan.** Present a table of fixes and reasons and wait for your confirmation.
5. **Install and verify.** Run pnpm install, re-run the audit script and pnpm run build:core.
6. **Look up advisories.** Record GHSA ID, CVE ID, severity and a one-line description per fix.
7. **Open the PR.** Commit as fix(deps) and open a PR with gh pr create.

Stop rule: Stops after one PR per run; no fixes are applied without your confirmation.

## Permissions

- Writes: package.json, **/package.json, loops/audit-dependencies-loop/**
- Network: github.com
- Sends: one pull request via gh pr create
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/audit-dependencies-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: audit check fails. Verification: you approve, audit exits 0. Memory: loops/audit-dependencies-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
