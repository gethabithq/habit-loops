---
name: mod-any-game
title: Mod Any Game skill
repo: rehan-remade/universal-modder
license: MIT
url: https://gethabit.dev/skills/rehan-remade/mod-any-game
---

# Mod Any Game skill

Mod any game is a skill for PC gamers and modders that takes a mod idea for a game they own to a working, recorded result: recon, route choice, safe lab, vertical slice, generated assets and in-game checks.

- Install the skill: `npx skills add rehan-remade/universal-modder --skill mod-any-game`
- Source: https://github.com/rehan-remade/universal-modder/tree/HEAD/.agents/skills/mod-any-game
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want new items in Terraria; You ask if a game can be modded; You plan a cross-game mashup.
Skip it when: The game is online with anti-cheat; You do not own the game.

# Make it a habit: Mods working in the real game.

For a game the user owns, your agent runs recon, picks the cheapest route, backs up saves, builds one vertical slice and verifies it in the running game with screenshots and logs. MODLOG.md keeps every path, failure and next step.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you name game, idea (manual; Claude Code; `manual: mod request for an owned game`)
- **Verification:** seen working in game. Hard checks: um backup create ran before the first modded launch; a screenshot and game log show the slice working; um publish check passes before sharing. On fail: stop, max 2 retries.
- **Memory:** mod journal at `MODLOG.md`. Read first: paths, IDs, chosen route, failures and the next step.

## Steps

1. **Intake.** Get the game, store and idea, agree what done means and start MODLOG.md.
2. **Recon.** Run um kb search and um scan, read the engine playbook, and use the game-recon skill.
3. **Pick the route.** Choose the cheapest route, such as data, loader API or patching, and log why.
4. **Set up the lab.** Run um backup create on saves and use a lab profile and windowed mode.
5. **Build a slice.** Take one item through with placeholder art, using the reverse-engineering skill to read real code.
6. **Verify in game.** Use game-automation with um win shot and logs, and stop after three repeats of one failure.
7. **Assets and showcase.** Make assets with fal-assets and asset-pipeline, then a clip with showcase-video.
8. **Publish and note.** Ask before publishing with publish-mod, then leave a field note with share-field-notes.

Stop rule: Stops after one vertical slice per run, or after three repeats of the same failure.

## Permissions

- Writes: MODLOG.md, MODDING_PLAN.md, examples/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`MODLOG.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you name game, idea. Verification: seen working in game. Memory: MODLOG.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
