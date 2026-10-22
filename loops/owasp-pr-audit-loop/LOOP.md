---
name: owasp-security-check
title: OWASP Security Check skill
repo: sergiodxa/agent-skills
license: MIT
url: https://gethabit.dev/skills/sergiodxa/owasp-security-check
---

# OWASP Security Check skill

Owasp security check is a skill for web developers that audits web apps and REST APIs against 20 rules based on the OWASP Top 10, from access control and injection to headers, CORS and rate limiting.

- Install the skill: `npx skills add sergiodxa/agent-skills --skill owasp-security-check`
- Source: https://github.com/sergiodxa/agent-skills/tree/HEAD/skills/owasp-security-check
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review code for vulnerabilities; You audit an API before release; You check auth and sessions.
Skip it when: You need a penetration test; The code is not a web app.

# Make it a habit: Security flaws caught before deploy.

On each pull request, your agent audits the changed code against 20 OWASP-based rules by priority, from access control and injection to headers and rate limits, and reports each finding with severity, file, impact and a code fix. It tracks open criticals.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened`)
- **Verification:** findings in full format. Hard checks: every finding has severity, category, file, issue, impact and fix; npm audit reports no critical vulnerability; no hardcoded secret pattern in changed files. On fail: notify, max 1 retries.
- **Memory:** security findings log at `loops/owasp-pr-audit-loop/run-log.md`. Read first: open critical and high findings.

## Steps

1. **Identify the app.** Decide if the change is a web app, REST API, SPA, SSR or mixed.
2. **Check critical rules.** Review access control, auth, data protection and input and output security first.
3. **Check high rules.** Review configuration, security headers, CORS, CSRF and sessions.
4. **Check medium rules.** Review API security, rate limiting, logging and dependencies with npm audit.
5. **Report.** Write each finding with severity, file, impact and a remediation code example.

Stop rule: Stops after one pull request per run, with one retry.

## Permissions

- Writes: loops/owasp-pr-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/owasp-pr-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: findings in full format. Memory: loops/owasp-pr-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
