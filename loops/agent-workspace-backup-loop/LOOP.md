---
name: openclaw-backup
title: OpenClaw Backup skill
repo: theagentservice/skills
license: MIT
url: https://gethabit.dev/skills/theagentservice/openclaw-backup
---

# OpenClaw Backup skill

The openclaw backup skill makes encrypted backups of OpenClaw agent workspace files, uploads them to soul-upload.com with a fresh password each time, and restores or deletes them. For people running OpenClaw agents.

- Install the skill: `npx skills add theagentservice/skills --skill openclaw-backup`
- Source: https://github.com/theagentservice/skills/tree/HEAD/openclaw-backup
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: backing up agent workspace files; restoring a previous agent backup; deleting an old remote backup.
Skip it when: you do not use OpenClaw; files must not leave your machine.

# Make it a habit: Agent files backed up, encrypted, restorable.

Once a week, your agent encrypts the OpenClaw workspace files with a fresh random password, uploads them with backup.py, and appends the backup id and password to the recovery file. Deletes only happen after you confirm.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly agent backup (schedule; cron; `0 3 * * 0`)
- **Verification:** upload returns backup id. Hard checks: the files to back up exist before upload; backup.py upload returns a backupId and sha256; the recovery file gains a new entry with the password; deletes run only after you confirm. On fail: notify, max 1 retries.
- **Memory:** backup recovery file at `.openclaw-backup-recovery.txt`. Read first: the list of earlier backup ids, dates and passwords.

## Steps

1. **Collect files.** Your agent uses your list or the default SOUL.md, MEMORY.md, IDENTITY.md, AGENTS.md and TOOLS.md, and checks they exist.
2. **Upload.** It runs backup.py upload without a password so a new random one is made.
3. **Record recovery.** It appends the backup id, password, URL, size and sha256 to the recovery file.
4. **Report.** It tells you the backup id and size and that the recovery file is needed to restore.
5. **Prune on request.** To delete an old backup it shows the list, asks you to confirm, then runs backup.py delete.

Stop rule: Stops after one backup per run, with at most one upload retry.

## Permissions

- Writes: .openclaw-backup-recovery.txt
- Network: soul-upload.com
- Sends: encrypted workspace archive to soul-upload.com
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.openclaw-backup-recovery.txt`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly agent backup. Verification: upload returns backup id. Memory: .openclaw-backup-recovery.txt. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
