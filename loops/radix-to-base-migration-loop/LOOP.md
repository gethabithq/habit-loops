---
name: migrate-radix-to-base
title: Migrate Radix to Base skill
repo: shadcn-ui/ui
license: MIT
url: https://gethabit.dev/skills/shadcn-ui/migrate-radix-to-base
---

# Migrate Radix to Base skill

The migrate radix to base skill moves shadcn wrappers and React code from Radix UI to Base UI step by step, with golden pairs, typechecks and a report per component. For teams switching their shadcn base library.

- Install the skill: `npx skills add shadcn-ui/ui --skill migrate-radix-to-base`
- Source: https://github.com/shadcn-ui/ui/tree/HEAD/skills/migrate-radix-to-base
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You move a shadcn project to Base UI; You migrate one Radix component; You need a report per component.
Skip it when: The project does not use Radix; You want a one-shot rewrite with no checks.

# Make it a habit: One component migrated per run.

Each day your agent migrates the next shadcn wrapper from Radix UI to Base UI in progressive mode: it writes a -base file, repoints consumers one by one, typechecks each step and commits. The .migration/ reports and the remaining Radix count are the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily migration step (schedule; Claude Code routine; `0 9 * * 1-5`)
- **Verification:** typecheck, build, no radix. Hard checks: typecheck passes after each consumer; build passes against the baseline; grep for radix-ui and @radix-ui is clean on the migrated files. On fail: stop, max 0 retries.
- **Memory:** migration reports at `.migration/<component>.md`. Read first: remaining wrappers on Radix and in-progress -base files.

## Steps

1. **Preflight.** Run npx shadcn@latest info --json, detect the package manager and require a clean tree.
2. **Baseline.** Run typecheck and build before touching dependencies.
3. **Pick the leaf.** Choose a wrapper whose own imports are already on Base UI.
4. **Golden pair.** Fetch the base variant by URL, or use the transformation engine for custom code.
5. **Write -base file.** Write <component>-base.tsx and keep the original untouched.
6. **Repoint consumers.** Move consumers one at a time with consumer-props.md and typecheck each.
7. **Finalize.** Delete the original, rename, commit, and write .migration/<component>.md.

Stop rule: Stops after one component per run.

## Permissions

- Writes: components/ui/**, .migration/**, components.json, package.json
- Network: ui.shadcn.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.migration/<component>.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily migration step. Verification: typecheck, build, no radix. Memory: .migration/<component>.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
