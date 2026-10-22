---
name: improve-codebase-architecture
title: Improve Codebase Architecture skill
repo: mattpocock/skills
license: MIT
url: https://gethabit.dev/skills/mattpocock/improve-codebase-architecture
---

# Improve Codebase Architecture skill

The improve codebase architecture skill by mattpocock scans a codebase for shallow modules, shows deepening candidates in a visual HTML report and grills you through the one you pick. For developers who want testable code.

- Install the skill: `npx skills add mattpocock/skills --skill improve-codebase-architecture`
- Source: https://github.com/mattpocock/skills/tree/HEAD/skills/engineering/improve-codebase-architecture
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your code feels hard to change; Tests are hard to write; You want a refactor plan.
Skip it when: The codebase is tiny; You need a quick bug fix.

# Make it a habit: Find shallow modules, deepen one.

Each week your agent scans recent hot spots from git log, finds shallow modules and writes an HTML report of deepening candidates. You pick one and it grills you through it, updating GLOSSARY.md and ADRs. A board keeps every candidate seen.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly architecture review (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** report check + your pick. Hard checks: the architecture-review HTML file exists in the temp dir; every candidate card has a recommendation strength badge; the report ends with a Top recommendation section. On fail: retry, max 1 retries.
- **Memory:** deepening candidates board at `loops/architecture-deepening-loop/board.md`. Read first: candidates already shown, picked or rejected, plus GLOSSARY.md and docs/adr/.

## Steps

1. **Load the vocabulary.** Your agent calls the codebase design skill for terms like module, seam, depth and leverage.
2. **Read the domain.** It reads GLOSSARY.md and the ADRs in docs/adr/ so it does not reopen settled decisions.
3. **Find hot spots.** Unless you named an area, it walks git log --oneline to see which files change most.
4. **Explore.** A sub-agent walks the code, notes friction and applies the deletion test to suspect modules.
5. **Write the report.** It writes a self-contained HTML report with one card and before/after diagram per candidate.
6. **Ask you.** It opens the report and asks which candidate you want to explore.
7. **Grill the pick.** It calls the grilling skill on your choice and the domain modeling skill to keep GLOSSARY.md current.
8. **Offer an ADR.** If you reject a candidate for a lasting reason, it offers to record that as an ADR.

Stop rule: Stops after one report and one picked candidate per run.

## Permissions

- Writes: $TMPDIR/architecture-review-*.html, GLOSSARY.md, docs/adr/**, loops/architecture-deepening-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/architecture-deepening-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly architecture review. Verification: report check + your pick. Memory: loops/architecture-deepening-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
