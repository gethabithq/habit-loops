---
name: asc-submission-health
title: ASC Submission Health skill
repo: rorkai/app-store-connect-cli-skills
license: MIT
url: https://gethabit.dev/skills/rorkai/asc-submission-health
---

# ASC Submission Health skill

ASC submission health diagnoses App Store submission blockers with the asc CLI, routes repairs, monitors review status and decides when to cancel or retry. For iOS and macOS developers whose release is blocked or stuck in review.

- Install the skill: `npx skills add rorkai/app-store-connect-cli-skills --skill asc-submission-health`
- Source: https://github.com/rorkai/app-store-connect-cli-skills/tree/HEAD/skills/asc-submission-health
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: asc validate reports blockers; a version is not in a valid state; review status looks stuck.
Skip it when: uploading or submitting a healthy build; you do not use the asc CLI.

# Make it a habit: Submission blockers found and routed.

When a release is blocked or review looks stuck, your agent runs asc validate and asc review doctor, gathers build and version evidence, routes each blocker to the right repair and watches review status. Cancels need your yes; a log keeps each diagnosis.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** validation fails or stalls (event; Claude Code routine; `asc validate reports blockers or review status unclear`)
- **Verification:** validators clean, you confirm. Hard checks: asc validate shows no blocking issues; attached build is VALID; asc validate iap or subscriptions show no blocking issues where relevant; asc status --until review-done exits 0. On fail: notify, max 1 retries.
- **Memory:** diagnosis log at `loops/app-review-health-loop/log.md`. Read first: last blockers found, repairs done and any SUBMISSION_ID.

## Steps

1. **Resolve the target.** Find APP_ID, version, BUILD_ID, platform and any SUBMISSION_ID, and stop if it is unclear.
2. **Diagnose.** Run asc validate and asc review doctor, then asc builds info and asc versions view for evidence.
3. **Route repairs.** Split blockers into public API, web-session and manual work, and fix one class at a time.
4. **Monitor review.** Use asc review status, asc submit status and asc review history to read the real state.
5. **Cancel only on yes.** Preview the submission, then run asc submit cancel with --confirm only after you agree.
6. **Hand back.** Re-run the validators and pass a healthy version to asc-release-flow for submission.

Stop rule: Stops after one version per run, with at most one re-validation after repairs.

## Permissions

- Writes: loops/app-review-health-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/app-review-health-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: validation fails or stalls. Verification: validators clean, you confirm. Memory: loops/app-review-health-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
