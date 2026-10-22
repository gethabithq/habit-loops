---
name: design-dna
title: Design DNA skill
repo: zanwei/design-dna
license: MIT
url: https://gethabit.dev/skills/zanwei/design-dna
---

# Design DNA skill

The design dna skill extracts a structured design profile from reference images or URLs across tokens, style and visual effects, then generates designs from it and verifies colors with a script. For designers and developers matching a look.

- Install the skill: `npx skills add zanwei/design-dna --skill design-dna`
- Source: https://github.com/zanwei/design-dna
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a style guide JSON from screenshots; You generate a page in a reference style; You need measured colors, not guesses.
Skip it when: You have a full design system already; You only need one color.

# Make it a habit: Match generated designs to references.

When you share reference designs, your agent measures colors with measure-colors.mjs, fills a full Design DNA JSON across system, style and effects, generates the design, screenshots it and runs verify.mjs until color drift passes. The DNA file is the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you share references (manual; Claude Code routine; `user gives images or URLs of a target style`)
- **Verification:** verify.mjs color drift. Hard checks: verify.mjs reports PASS on per-color ΔE and coverage; every schema field in the DNA JSON is filled; generated HTML file exists. On fail: retry, max 2 retries.
- **Memory:** Design DNA JSON at `loops/design-dna-fidelity-loop/design-dna.json`. Read first: the DNA JSON and its measured_palette.

## Steps

1. **Read the schema.** Your agent reads references/schema.md for all fields.
2. **Measure colors.** For image references it runs measure-colors.mjs instead of guessing hex values.
3. **Extract DNA.** It fills design_system, design_style and visual_effects for every field.
4. **Confirm values.** It asks if you want to adjust any values before generating.
5. **Generate.** It follows references/generation-guide.md to build HTML with tokens and effects.
6. **Verify.** It screenshots the output, runs verify.mjs and fixes failing colors.

Stop rule: Stops after one design and 2 verify-fix rounds per run.

## Permissions

- Writes: loops/design-dna-fidelity-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/design-dna-fidelity-loop/design-dna.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you share references. Verification: verify.mjs color drift. Memory: loops/design-dna-fidelity-loop/design-dna.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
