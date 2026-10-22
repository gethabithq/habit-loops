---
name: layer-game-assets
title: Layer Game Assets skill
repo: layerai/skills
license: MIT
url: https://gethabit.dev/skills/layerai/layer-game-assets
---

# Layer Game Assets skill

The layer game assets skill produces in-game art on Layer that fits a system: on-model character casts, rig-ready characters, parallax backgrounds and icon sets that read at small size. For game studios building asset sets.

- Install the skill: `npx skills add layerai/skills --skill layer-game-assets`
- Source: https://github.com/layerai/skills/tree/HEAD/skills/layer-game-assets
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: extending a character cast; making an icon set that reads at 64px; building parallax background layers.
Skip it when: you need a single standalone illustration; you make pixel art.

# Make it a habit: New assets that match the set.

When a set grows, your agent generates each new character, icon or background against approved anchors, names the shared grammar in every prompt, and reviews the set at target size. A log keeps anchor file ids and the grammar.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** set needs new assets (event; Claude Code routine; `request to extend a cast, icon set or background`)
- **Verification:** on-model at target size. Hard checks: every run attaches the approved anchors as reference_image; each prompt names the shared grammar and background treatment; icons are reviewed together at their target pixel size. On fail: retry, max 2 retries.
- **Memory:** set grammar notes at `loops/game-asset-set-loop/set.md`. Read first: approved anchor file ids and the shared stroke, palette and perspective.

## Steps

1. **Load anchors.** Your agent takes the file ids of the approved assets in the set.
2. **Choose model.** It calls list_base_models with image_editing and any needed shape capability.
3. **Write prompt.** It names role, silhouette, view, background and the shared grammar, plus the one new subject.
4. **Confirm first.** It estimates and runs the first asset, and you confirm the look.
5. **Run the rest.** It runs one generation per remaining asset with the same anchors.
6. **Review together.** It reviews the set side by side at the target size and rerolls outliers.

Stop rule: Stops after one requested set per run, with at most two rerolls per asset.

## Permissions

- Writes: loops/game-asset-set-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/game-asset-set-loop/set.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: set needs new assets. Verification: on-model at target size. Memory: loops/game-asset-set-loop/set.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
