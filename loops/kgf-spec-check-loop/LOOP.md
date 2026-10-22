---
name: indexion-kgf
title: Indexion KGF skill
repo: trkbt10/indexion-skills
license: Apache-2.0
url: https://gethabit.dev/skills/trkbt10/indexion-kgf
---

# Indexion KGF skill

Indexion kgf inspects and debugs KGF language specs by showing tokens, parse events and extracted edges for a source file, with known PEG and token pitfalls. For developers adding or fixing language support in indexion.

- Install the skill: `npx skills add trkbt10/indexion-skills --skill indexion-kgf`
- Source: https://github.com/trkbt10/indexion-skills/tree/HEAD/skills/indexion-kgf
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You write a new KGF spec; A grep pattern does not match; Doc comments go missing in output.
Skip it when: You only use indexion's high-level commands; Your project does not use indexion.

# Make it a habit: KGF spec edits keep docs extracted.

When a KGF spec file changes, your agent runs indexion kgf inspect on a sample file, drills into tokens, events and edges, and checks that declares edges still carry doc. It looks for the known PEG ordering, NL and token priority pitfalls.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** KGF spec changes (event; GitHub Actions or Claude Code routine; `push paths: kgfs/*.kgf`)
- **Verification:** doc in declares edges. Hard checks: indexion kgf edges on the sample file shows declares edges; each declares edge for a documented item shows doc=; indexion kgf inspect runs without errors. On fail: retry, max 2 retries.
- **Memory:** spec check log at `loops/kgf-spec-check-loop/log.md`. Read first: sample files per spec and pitfalls found before.

## Steps

1. **Inspect the sample.** Run indexion kgf inspect with the changed spec on a sample file.
2. **Drill down.** Use indexion kgf tokens, events or edges for the part that looks wrong.
3. **Check pitfalls.** Look for DocComment ordered before declarations, a missing NL? and generic tokens defined before specific ones.
4. **Verify doc extraction.** Run indexion kgf edges and grep declares to confirm doc is present.
5. **Log the result.** Record the spec, the sample file and any pitfall fixed.

Stop rule: Stops after one changed spec per run, with at most 2 retries.

## Permissions

- Writes: kgfs/**, loops/kgf-spec-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/kgf-spec-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: KGF spec changes. Verification: doc in declares edges. Memory: loops/kgf-spec-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
