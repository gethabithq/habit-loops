---
name: asc-release-flow
title: ASC release flow skill
repo: rorkai/app-store-connect-cli-skills
license: MIT
url: https://gethabit.dev/skills/rorkai/asc-release-flow
---

# ASC release flow skill

The asc release flow skill carries an App Store release from plan to review with the asc CLI: staging metadata, attaching a build, publishing an IPA and submitting, for iOS developers.

- Install the skill: `npx skills add rorkai/app-store-connect-cli-skills --skill asc-release-flow`
- Source: https://github.com/rorkai/app-store-connect-cli-skills/tree/HEAD/skills/asc-release-flow
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: submitting a new app version; uploading an IPA to App Store; staging metadata for a release.
Skip it when: a submission is stuck or rejected; cancelling a submission.

# Make it a habit: Releases reach review safely.

Runs when a release is approved. Your agent stages the version with asc, validates it, previews every change with a dry run, waits for your confirm, then submits and records the submission IDs for the next release.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** release approved (manual; Claude Code; `user starts a release`)
- **Verification:** validate plus your confirm. Hard checks: asc validate reports no blocking issues; dry-run plan matches the requested release; no second review submission for the version. On fail: stop, max 0 retries.
- **Memory:** release handoff log at `loops/asc-release-loop/releases.md`. Read first: last release IDs and the lane that ran.

## Steps

1. **Resolve targets.** Find APP_ID, the version, BUILD_ID and platform, and check asc auth login.
2. **Choose the lane.** Pick asc release stage, asc review submit or asc publish appstore.
3. **Stage and validate.** Stage the build, then run asc validate and stop at any failing gate.
4. **Route blockers.** Send non-Game Center blockers and digital goods checks to asc-submission-health.
5. **Dry run.** Run the chosen command with --dry-run and show you the plan.
6. **Confirm with you.** Ask you to approve before rerunning with --confirm.
7. **Hand off.** Record app, version, build and submission IDs plus the monitor command.

Stop rule: Stops after one release per run, with no retries after a failed gate.

## Permissions

- Writes: ./metadata/**, loops/asc-release-loop/**
- Network: none
- Sends: App Store review submission
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/asc-release-loop/releases.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: release approved. Verification: validate plus your confirm. Memory: loops/asc-release-loop/releases.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
