---
name: baoyu-image-gen
title: Baoyu Image Gen skill
repo: JimLiu/baoyu-skills
license: MIT
url: https://gethabit.dev/skills/jimliu/baoyu-image-gen
---

# Baoyu Image Gen skill

The baoyu image gen skill generates images through many provider APIs, with reference images, aspect ratios, quality presets and parallel batch runs from saved prompts. For creators and developers who need images from an agent.

- Install the skill: `npx skills add JimLiu/baoyu-skills --skill baoyu-image-gen`
- Source: https://github.com/JimLiu/baoyu-skills/tree/HEAD/skills/baoyu-image-gen
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need images from text prompts; You have many saved prompts to render; You need reference-image edits.
Skip it when: You need vector or SVG output; You have no provider access.

# Make it a habit: Saved prompts become finished images.

When new prompt files land in prompts/, your agent loads EXTEND.md, builds a batch file with build-batch.ts and runs main.ts in batch mode. Each image retries up to three times. The run reports success and failure counts, kept in a log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new prompt files saved (event; Claude Code routine; `new files in prompts/`)
- **Verification:** every image exists. Hard checks: EXTEND.md exists before generation; failure count in the batch output is zero; every output image path exists. On fail: notify, max 0 retries.
- **Memory:** batch results log at `loops/image-batch-loop/runs.md`. Read first: prompts already rendered and past failure reasons.

## Steps

1. **Load preferences.** Read EXTEND.md, and stop the run if first-time setup has not created it yet.
2. **Show the model.** Print which provider and model will be used.
3. **Build the batch.** Run build-batch.ts with the outline and prompts to write batch.json.
4. **Generate.** Run main.ts with --batchfile and --jobs.
5. **Check results.** Read success and failure counts and per-image reasons.

Stop rule: Stops after one batch file per run; each image gets at most 3 attempts.

## Permissions

- Writes: attachments/**, batch.json, loops/image-batch-loop/**
- Network: provider image API set in EXTEND.md
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/image-batch-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new prompt files saved. Verification: every image exists. Memory: loops/image-batch-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
