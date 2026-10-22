---
name: tigris-security-access-control
title: Tigris Security Access Control skill
repo: tigrisdata/skills
license: MIT
url: https://gethabit.dev/skills/tigrisdata/tigris-security-access-control
---

# Tigris Security Access Control skill

The tigris security access control skill covers access key lifecycle, bucket roles, CORS rules, public and private buckets, presigned URL safety and a security audit checklist for Tigris object storage. For developers securing storage.

- Install the skill: `npx skills add tigrisdata/skills --skill tigris-security-access-control`
- Source: https://github.com/tigrisdata/skills/tree/HEAD/skills/tigris-security-access-control
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you rotate access keys; browser uploads fail on CORS; you audit storage security.
Skip it when: you only upload files; you use another storage provider.

# Make it a habit: Storage keys and CORS stay tight.

Once a month the agent runs the Tigris security checklist: no tid_ or tsec_ strings in the repo, .env in .gitignore, keys scoped to buckets with the right role, no wildcard CORS with write methods. It asks before revoking keys and logs each audit.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly storage security audit (schedule; cron or Claude Code routine; `0 9 1 * *`)
- **Verification:** audit checklist + your OK. Hard checks: search for tid_ and tsec_ in the repo finds zero matches; .env is listed in .gitignore; tigris buckets cors get shows no "*" origin with PUT or DELETE; every key in tigris access-keys list is assigned to a bucket. On fail: notify, max 0 retries.
- **Memory:** security audit log at `loops/tigris-security-audit-loop/log.md`. Read first: keys, roles and CORS rules from the last audit and open findings.

## Steps

1. **Read last audit.** Open the log for the last key list, CORS rules and open findings.
2. **Scan for secrets.** Search the repo for tid_ and tsec_ and confirm .env is in .gitignore.
3. **Review access keys.** Run tigris access-keys list and tigris access-keys info to check bucket scope and roles.
4. **Review CORS rules.** Run tigris buckets cors get for each bucket and flag wildcard origins with write methods.
5. **Check presigned expiry.** Look for presigned URLs in code with expiresIn above one hour.
6. **Ask before revoking.** List stale or over-scoped keys and ask you before running tigris access-keys delete.
7. **Log the audit.** Write findings, fixes and keys due for rotation into the log.

Stop rule: One audit per run, no key deleted without your OK.

## Permissions

- Writes: loops/tigris-security-audit-loop/, cors.json
- Network: t3.storage.dev
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/tigris-security-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly storage security audit. Verification: audit checklist + your OK. Memory: loops/tigris-security-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
