---
name: layer-art-direction
title: Layer Art Direction skill
repo: layerai/skills
license: MIT
url: https://gethabit.dev/skills/layerai/layer-art-direction
---

# Layer Art Direction skill

The layer art direction skill sets a direction before volume generation on Layer: production-term style names, single-axis moodboards, palettes, framing and storyboards. For game and marketing teams briefing AI asset work.

- Install the skill: `npx skills add layerai/skills --skill layer-art-direction`
- Source: https://github.com/layerai/skills/tree/HEAD/skills/layer-art-direction
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: exploring a look with a moodboard; storyboarding a trailer or cutscene; a brief keeps missing its intent.
Skip it when: the look is already approved; you need a single quick image.

# Make it a habit: An agreed look before volume generation.

Before a big batch, your agent turns the brief into production terms, runs one moodboard that varies a single axis, and asks you to pick a direction. The chosen image becomes the anchor for every later run, kept in a notes file.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new brief arrives (event; Claude Code routine; `a new asset or trailer brief`)
- **Verification:** you pick a direction. Hard checks: the moodboard varies exactly one axis; you confirm one direction before volume generation; later runs attach the chosen anchor as reference_image. On fail: notify, max 1 retries.
- **Memory:** direction notes at `loops/art-direction-signoff-loop/direction.md`. Read first: the approved style terms, palette and anchor image.

## Steps

1. **Translate brief.** Your agent turns vague style words into production terms and reads them back to you.
2. **Pin palette.** It sets a named colour count and relationship, with value contrast for readability.
3. **Run moodboard.** It runs one moodboard with the same subject and palette, varying one axis.
4. **Pick direction.** It asks you which direction to pursue.
5. **Storyboard.** For a trailer it writes the beats as a list and makes panels that each advance the story.
6. **Anchor.** It attaches the chosen image as reference_image to every later run.

Stop rule: Stops after one direction is approved, with at most one more moodboard.

## Permissions

- Writes: loops/art-direction-signoff-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/art-direction-signoff-loop/direction.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new brief arrives. Verification: you pick a direction. Memory: loops/art-direction-signoff-loop/direction.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
