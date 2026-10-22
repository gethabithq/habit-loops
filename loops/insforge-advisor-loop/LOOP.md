---
name: insforge-cli
title: InsForge CLI skill
repo: InsForge/insforge-skills
license: Apache-2.0
url: https://gethabit.dev/skills/insforge/insforge-cli
---

# InsForge CLI skill

The insforge cli skill lets your agent run an InsForge backend from the command line: projects, SQL migrations, RLS, functions, storage, backups, deployments, secrets, schedules, logs, advisor scans, branches and agent memory. For developers who manage InsForge infrastructure.

- Install the skill: `npx skills add InsForge/insforge-skills --skill insforge-cli`
- Source: https://github.com/InsForge/insforge-skills/tree/HEAD/skills/insforge-cli
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You need a backend for an app; You write migrations or RLS policies; You check advisor findings or logs.
Skip it when: You only write app code with @insforge/sdk; You do not use InsForge.

# Make it a habit: Clear backend advisor findings weekly.

Each week your agent recalls project memory, runs an InsForge advisor scan, fixes security and performance findings through migrations on a backend branch, and merges only after a dry run and your OK. It rescans and records decisions in project memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly advisor scan (schedule; Claude Code routine or GitHub Actions; `0 7 * * 1`)
- **Verification:** rescan + your merge OK. Hard checks: diagnose advisor --json shows scan.status completed for the scanId that advisor scan returned; every CLI call exits with code 0; branch merge --dry-run succeeds before the real merge; the rescan shows fewer critical findings than the first scan; no finding was suppressed without your judgement. On fail: stop, max 1 retries.
- **Memory:** advisor runs log at `loops/insforge-advisor-loop/log.md`. Read first: npx -y @insforge/cli memory list, then last week's findings and fixes.

## Steps

1. **Recall memory.** Run npx -y @insforge/cli memory list and recall titles that match the findings.
2. **Scan.** Run advisor scan and poll diagnose advisor --json until the scan is completed.
3. **Branch.** Create a backend branch with branch create <name> --mode schema-only for risky fixes.
4. **Fix with migrations.** Write each fix with db migrations new <name> and apply it with db migrations up --all on the branch.
5. **Review the merge.** Run branch merge <name> --dry-run, show you the SQL and wait for your yes.
6. **Merge and rescan.** Merge the branch, run advisor scan again and compare the findings.
7. **Remember.** Store decisions and gotchas with memory remember, and log the run.

Stop rule: Stops after the critical findings of one scan per run, with one retry of the rescan.

## Permissions

- Writes: migrations/**, loops/insforge-advisor-loop/**
- Network: api.insforge.dev
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/insforge-advisor-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly advisor scan. Verification: rescan + your merge OK. Memory: loops/insforge-advisor-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
