---
name: printing-press-reprint
title: Printing Press Reprint skill
repo: mvanhorn/cli-printing-press
license: MIT
url: https://gethabit.dev/skills/mvanhorn/printing-press-reprint
---

# Printing Press Reprint skill

The printing press reprint skill regenerates an existing printed CLI under the current Printing Press, carrying prior research, novel features and patches into the new run. For people who maintain CLIs made with cli-printing-press.

- Install the skill: `npx skills add mvanhorn/cli-printing-press --skill printing-press-reprint`
- Source: https://github.com/mvanhorn/cli-printing-press/tree/HEAD/skills/printing-press-reprint
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A Printing Press upgrade would help a CLI; A published CLI has a known gap; You want prior features re-evaluated.
Skip it when: You only need a small code fix; Local work is not yet published.

# Make it a habit: Regenerate CLIs after machine upgrades.

When the Printing Press gets a big upgrade, your agent reconciles a CLI's local and public copies, gathers prior research and patches, recommends reuse or redo by research age, offers scorecard-based enrichment and hands off to /printing-press.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Printing Press upgrade lands (event; Claude Code routine; `new cli-printing-press version, or /printing-press-reprint <cli>`)
- **Verification:** your choices, clean handoff. Hard checks: stops if the local copy has newer unpublished work; patch count is read from both patch index shapes; handoff names research mode reuse or redo. On fail: stop, max 0 retries.
- **Memory:** prior research and patches at `$PRESS_LIBRARY/<slug>/.printing-press-patches/`. Read first: prior research.json age and recorded patches.

## Steps

1. **Resolve presence.** Your agent matches the CLI in registry.json and compares local and public run_id and generated_at.
2. **Import if needed.** If only the public copy exists, it runs /printing-press-import first.
3. **Gather prior context.** It finds research.json and fetches patches in either index shape.
4. **Recommend research.** It shows research age and machine version and asks reuse, redo or show first.
5. **Offer enrichment.** It reads the prior scorecard and asks about MCP or auth enrichment for weak dimensions.
6. **Hand off.** It invokes /printing-press with the reason, research mode, enrichment and prior patches.

Stop rule: Stops after one CLI handoff per run.

## Permissions

- Writes: $PRESS_LIBRARY/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`$PRESS_LIBRARY/<slug>/.printing-press-patches/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Printing Press upgrade lands. Verification: your choices, clean handoff. Memory: $PRESS_LIBRARY/<slug>/.printing-press-patches/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
