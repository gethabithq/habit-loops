---
name: php-best-practices
title: PHP Best Practices skill
repo: asyrafhussin/agent-skills
license: MIT
url: https://gethabit.dev/skills/asyrafhussin/php-best-practices
---

# PHP Best Practices skill

PHP Best Practices reviews PHP 8.x code against type safety, modern features, PSR standards, SOLID principles, error handling, performance and security rules, matched to the project's version. For PHP developers auditing code.

- Install the skill: `npx skills add asyrafhussin/agent-skills --skill php-best-practices`
- Source: https://github.com/asyrafhussin/agent-skills/tree/HEAD/skills/php-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: reviewing or auditing PHP code; checking type safety in PHP; ensuring PSR and SOLID compliance.
Skip it when: the project is not PHP; you want automated refactoring instead of review.

# Make it a habit: PHP code checked against modern rules.

When PHP changes, your agent detects the project's PHP version, then audits the code against the type, modern, PSR, SOLID, error, performance and security rules, and reports findings as file:line notes. A run log keeps prior findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PHP code changes (event; GitHub Actions or Claude Code routine; `push touching .php files`)
- **Verification:** version-aware findings. Hard checks: the project PHP version is read from composer.json or php -v; no suggestion uses syntax newer than that version; findings are listed as file:line with a category. On fail: notify, max 1 retries.
- **Memory:** audit findings log at `loops/php-audit-loop/run-log.md`. Read first: the detected PHP version and prior findings.

## Steps

1. **Detect version.** Your agent reads the required PHP version from composer.json and checks php -v.
2. **Check types.** It checks strict types, return, parameter and property types against the type rules.
3. **Check modern features.** It flags where enums, match, readonly and other version-appropriate features fit.
4. **Check PSR and SOLID.** It checks PSR-4, PSR-12, naming and the five SOLID principles.
5. **Check errors and security.** It checks exception handling, prepared statements, output escaping and password hashing.
6. **Report.** It writes each finding as file:line with its category to the run log.

Stop rule: Stops after one change set per run, with at most one re-scan.

## Permissions

- Writes: loops/php-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/php-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PHP code changes. Verification: version-aware findings. Memory: loops/php-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
