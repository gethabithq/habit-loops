---
name: lark-drive
title: Lark Drive skill
repo: larksuite/cli
license: MIT
url: https://gethabit.dev/skills/larksuite/lark-drive
---

# Lark Drive skill

The lark drive skill manages Feishu and Lark Drive through lark-cli: upload and download, folders, copy, move and delete, comments, permissions, versions, secure labels, search and importing local files as docs, sheets, Base or slides.

- Install the skill: `npx skills add larksuite/cli --skill lark-drive`
- Source: https://github.com/larksuite/cli/tree/HEAD/skills/lark-drive
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You sync or organize Drive folders; You import Excel, CSV or Markdown into Lark; You audit sharing and permissions.
Skip it when: You edit document text (use lark-doc); You change cells or Base records (use lark-sheets or lark-base).

# Make it a habit: Local folder matches Drive.

On a schedule, your agent compares a local folder with a Drive folder using +status, shows you the plan, runs +sync after your OK and runs +status again to confirm nothing differs. A run log keeps what moved in each direction.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly folder sync (schedule; Claude Code routine; `0 22 * * *`)
- **Verification:** status diff plus OK. Hard checks: second +status run shows no new_local, new_remote or modified files; sync result returns ok == true; no import retried more than 3 times. On fail: notify, max 1 retries.
- **Memory:** sync history at `loops/lark-drive-sync-loop/run-log.md`. Read first: last folder token, conflict policy and files synced.

## Steps

1. **Read shared rules.** The agent first reads the lark-shared skill for auth and permission handling.
2. **Compare folders.** +status lists the differences between the local directory and the Drive folder by SHA-256.
3. **Plan and confirm.** It lists the files and the --on-conflict choice, and waits for your explicit OK because a batch sync is a high-risk write.
4. **Sync.** +sync pulls new remote files, pushes new local files and handles modified ones by the chosen policy.
5. **Check again.** A second +status run must show no differences, and the run log records what moved.

Stop rule: Stops after one folder pair per run; on not found, permission denied or missing scope it stops without retry.

## Permissions

- Writes: loops/lark-drive-sync-loop/**, the synced local folder
- Network: Lark Drive API via lark-cli
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/lark-drive-sync-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly folder sync. Verification: status diff plus OK. Memory: loops/lark-drive-sync-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
