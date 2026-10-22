---
name: nanobanana
title: Nano Banana skill
repo: GargantuaX/openskills
license: MIT
url: https://gethabit.dev/skills/gargantuax/nanobanana
---

# Nano Banana skill

The nano banana skill gives agents one Python script for Gemini-native image generation and editing, with model aliases, strict option checks, batch runs and custom gateways, for developers and designers who need images on demand.

- Install the skill: `npx skills add GargantuaX/openskills --skill nanobanana`
- Source: https://github.com/GargantuaX/openskills/tree/HEAD/skills/nanobanana
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need text-to-image or image edits; You want several variants in one batch; You use a Gemini-compatible gateway.
Skip it when: You need video or audio; You cannot use a Gemini API key.

# Make it a habit: Fresh images from every prompt.

When a new image prompt lands, your agent checks the request with --dry-run, then runs scripts/nanobanana.py generate or batch. A hard check confirms every image file exists, and a log keeps prompts, models and options.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new image prompt added (event; Claude Code routine; `new prompt entry in the loop board`)
- **Verification:** dry run + files exist. Hard checks: --dry-run request passes the strict option validation; every output image file exists after the run; batch run saves as many files as --count asks for. On fail: retry, max 1 retries.
- **Memory:** prompt and model log at `loops/nanobanana-image-loop/run-log.md`. Read first: past prompts, chosen model aliases and options that the script rejected.

## Steps

1. **Read the config.** Open references/config.md and references/models-and-api.md to set environment variables and pick a tier.
2. **Pick a model.** Use nanobanana-2 by default, nanobanana for speed or nanobanana-pro for the best fidelity.
3. **Dry run.** Add --dry-run to inspect the payload, endpoint and model options before sending.
4. **Generate.** Run scripts/nanobanana.py generate for one image or batch for several variants, with --input-image for edits.
5. **Check files.** Confirm each image file exists in the loop folder and the count matches.
6. **Log the run.** Write the prompt, model alias, ratio and size to the run log without any secrets.

Stop rule: One prompt per run, at most one batch of variants, one retry.

## Permissions

- Writes: loops/nanobanana-image-loop/**
- Network: generativelanguage.googleapis.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nanobanana-image-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new image prompt added. Verification: dry run + files exist. Memory: loops/nanobanana-image-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
