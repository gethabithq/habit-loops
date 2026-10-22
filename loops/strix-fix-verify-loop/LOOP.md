---
name: fix-security-vulnerabilities-with-strix
title: Fix Security Vulnerabilities with Strix skill
repo: usestrix/strix
license: Apache-2.0
url: https://gethabit.dev/skills/usestrix/fix-security-vulnerabilities-with-strix
---

# Fix Security Vulnerabilities with Strix skill

The fix security vulnerabilities with strix skill helps your agent patch findings from a Strix pentest at the root cause and re-run Strix to prove each fix works. For developers who scan with the Strix CLI or the Strix cloud.

- Install the skill: `npx skills add usestrix/strix --skill fix-security-vulnerabilities-with-strix`
- Source: https://github.com/usestrix/strix/tree/HEAD/skills/fix-security-vulnerabilities-with-strix
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: A Strix scan reported findings; You fix injection, XSS or IDOR issues; You need proof a fix closes the exploit.
Skip it when: You have no Strix scan results; You only want a scan, not fixes.

# Make it a habit: Findings fixed and proven closed.

When a Strix scan reports findings, your agent fixes them by severity at the root cause, then re-runs Strix and the PoC to prove each one is closed. It runs the test suite and keeps a per-finding report for the next scan.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Strix scan reports findings (event; GitHub Actions or Claude Code routine; `new strix_runs/<run-name>/vulnerabilities.json or cloud scan with findings`)
- **Verification:** re-scan clean, tests pass. Hard checks: strix re-scan exits with code 0; run.json shows a completed status; the original PoC no longer reproduces; the project's test suite passes. On fail: retry, max 2 retries.
- **Memory:** per-finding fix report at `loops/strix-fix-verify-loop/report.md`. Read first: findings still open after the last scan.

## Steps

1. **Collect findings.** Your agent reads vulnerabilities.json in strix_runs, or pulls cloud findings with strix cloud vulns list.
2. **Triage.** It orders the findings from critical to low and treats each as real until the PoC is re-tested.
3. **Reproduce.** It replays the PoC from the finding file when that is feasible.
4. **Fix the root cause.** It applies a small fix that uses the framework's built-in defense and the repo's patterns.
5. **Re-scan.** It re-runs strix with --scope-mode diff or a focused --instruction, or reruns the cloud scan.
6. **Run tests.** It runs the project's own test suite to catch broken behavior.
7. **Report.** It writes severity, root cause, fix location and result per finding, and marks verified cloud findings fixed.

Stop rule: Stops after 5 findings per run and 2 re-scan retries per finding.

## Permissions

- Writes: src/**, loops/strix-fix-verify-loop/**
- Network: app.strix.ai
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/strix-fix-verify-loop/report.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Strix scan reports findings. Verification: re-scan clean, tests pass. Memory: loops/strix-fix-verify-loop/report.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
