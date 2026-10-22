---
name: share-field-notes
title: Share Field Notes skill
repo: rehan-remade/universal-modder
license: MIT
url: https://gethabit.dev/skills/rehan-remade/share-field-notes
---

# Share Field Notes skill

Share field notes is a skill for modding agents that searches a shared knowledge base before work and, at the end, writes a field note with versions, route, engine facts and gotchas, then opens a PR with the human's OK.

- Install the skill: `npx skills add rehan-remade/universal-modder --skill share-field-notes`
- Source: https://github.com/rehan-remade/universal-modder/tree/HEAD/.agents/skills/share-field-notes
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ask if a game was modded; You hit an engine quirk; A modding session ends.
Skip it when: The work is not about games; You cannot share what you learned.

# Make it a habit: Every modding session leaves a note.

Before modding, your agent searches the shared knowledge base. During work it keeps MODLOG.md. At the end it turns the journal into a field note, runs um kb check and, with your OK, opens a pull request so the next agent benefits.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** modding session ends (event; Claude Code; `event: end of a modding session`)
- **Verification:** kb check, your OK. Hard checks: um kb check passes on the note; um kb index runs; um kb pr --yes runs only after the human agrees. On fail: stop, max 1 retries.
- **Memory:** mod journal at `MODLOG.md`. Read first: versions, paths, failures and what was verified.

## Steps

1. **Search first.** Run um kb search for the game and engine before starting.
2. **Keep the journal.** Log versions, paths, IDs, failures and checks in MODLOG.md.
3. **Write the note.** Run um kb new and fill setup, engine facts, verification and numbered gotchas.
4. **Extend, don't duplicate.** Add to an existing note for the same game instead of writing a new one.
5. **Check.** Run um kb check and um kb index.
6. **Ask, then PR.** Show the human the note, run um kb pr as a dry run, then --yes on approval.

Stop rule: Stops after one note per session, with one fix round.

## Permissions

- Writes: MODLOG.md, knowledge/**
- Network: github.com, raw.githubusercontent.com
- Sends: public pull request, only after the human agrees
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`MODLOG.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: modding session ends. Verification: kb check, your OK. Memory: MODLOG.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
