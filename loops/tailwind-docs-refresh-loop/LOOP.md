---
name: tailwind-4-docs
title: Tailwind 4 Docs skill
repo: Lombiq/Tailwind-Agent-Skills
license: BSD-3-Clause
url: https://gethabit.dev/skills/lombiq/tailwind-4-docs
---

# Tailwind 4 Docs skill

The tailwind 4 docs skill gives agents a local snapshot of the official Tailwind CSS v4 documentation, for developers answering v4 questions, choosing utilities and variants, or migrating projects from v3 to v4.

- Install the skill: `npx skills add Lombiq/Tailwind-Agent-Skills --skill tailwind-4-docs`
- Source: https://github.com/Lombiq/Tailwind-Agent-Skills/tree/HEAD/skills/tailwind-4-docs
- Licence: BSD-3-Clause (Habit links to this skill and does not host or change it)

Use it when: Answering Tailwind v4 questions from official docs; Migrating a project from v3 to v4; Reviewing Tailwind code against the docs.
Skip it when: You have no git, Python or internet for the first sync; Your project stays on Tailwind v3.

# Make it a habit: Tailwind v4 docs never go stale.

Once a week the agent reads the snapshot date in references/docs-source.txt. If the snapshot is missing or older than one week, it asks you, runs the sync script and checks that references/docs/ and references/docs-index.tsx exist.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine; `0 7 * * 1`)
- **Verification:** you approve + files exist. Hard checks: references/docs/ exists and is not empty; references/docs-index.tsx exists; references/docs-source.txt shows a snapshot date less than one week old. On fail: notify, max 1 retries.
- **Memory:** snapshot source file at `references/docs-source.txt`. Read first: the upstream commit and date of the last snapshot.

## Steps

1. **Check the snapshot.** The agent looks for references/docs/ and references/docs-index.tsx.
2. **Read the age.** It reads the snapshot date in references/docs-source.txt.
3. **Ask first.** If the snapshot is missing or older than one week, it asks you before syncing.
4. **Sync.** It runs scripts/sync_tailwind_docs.py with --accept-docs-license, adding --local-repo when a clone exists.
5. **Verify files.** It confirms both generated paths exist after the sync.
6. **Fall back.** If the sync is blocked, it uses references/gotchas.md and says the guidance is limited.

Stop rule: Stops after one sync attempt and at most 1 retry per run.

## Permissions

- Writes: references/docs/**, references/docs-index.tsx, references/docs-source.txt
- Network: tailwindcss.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`references/docs-source.txt`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: you approve + files exist. Memory: references/docs-source.txt. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
