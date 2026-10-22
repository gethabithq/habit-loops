---
name: devboxes
title: Devboxes skill
repo: namespacelabs/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/namespacelabs/devboxes
---

# Devboxes skill

Devboxes is a skill for developers who create, run, share and tear down Namespace devboxes with devbox or boxctl, for isolated Linux or macOS builds, remote tests, Docker hosts and shared devbox.so URLs.

- Install the skill: `npx skills add namespacelabs/agent-skills --skill devboxes`
- Source: https://github.com/namespacelabs/agent-skills/tree/HEAD/skills/devboxes
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Tests need more than your laptop; You need a macOS or Linux box; You share a dev server with teammates.
Skip it when: The task runs fine locally; You do not use Namespace.

# Make it a habit: Tests run on a disposable devbox.

For each pull request, your agent creates an ephemeral Namespace devbox, syncs the working tree including untracked files, runs the tests with a small summary line and tears the box down. Logs stay on the box unless the run fails.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; Claude Code routine; `pull_request.opened`)
- **Verification:** exit code and cleanup. Hard checks: the run summary prints exit=0; devbox exec ls shows the synced files; boxctl task list shows no leftover markers; devbox expire --force succeeds. On fail: retry, max 1 retries.
- **Memory:** devbox run log at `loops/devbox-test-run-loop/run-log.md`. Read first: image and size that worked last time.

## Steps

1. **Preflight.** Check NAMESPACE_DEVBOX_WORKSPACE_DIR, resolve devbox and run auth check-login, with devbox login if needed.
2. **Create the box.** Run devbox create with --ephemeral, an image from devbox image list and a fitting size.
3. **Ask on limits.** If plan limits block creation, run devbox list and ask the user which box to reuse or expire.
4. **Sync the tree.** Upload or tar the working tree, or apply a patch plus untracked files from git ls-files.
5. **Run the tests.** Upload a run script, chmod it and run it with devbox exec, logging to /workspaces/run.log.
6. **Fetch on failure.** Use devbox download for the log only when the summary shows a non-zero exit.
7. **Tear down.** Clear any boxctl task markers and run devbox expire --force.

Stop rule: Stops after one test run per pull request, with one retry.

## Permissions

- Writes: loops/devbox-test-run-loop/**
- Network: cloud.namespace.so, devbox.so, github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/devbox-test-run-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: exit code and cleanup. Memory: loops/devbox-test-run-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
