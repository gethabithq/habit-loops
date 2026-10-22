---
name: refero-design
title: Refero Design skill
repo: referodesign/refero_skill
license: MIT
url: https://gethabit.dev/skills/referodesign/refero-design
---

# Refero Design skill

The refero design skill gives agents a research-first method for UI, product and web design. It grounds every choice in Refero styles, screens and flows, then locks a direction. For teams that want designs that do not look generic.

- Install the skill: `npx skills add referodesign/refero_skill --skill refero-design`
- Source: https://github.com/referodesign/refero_skill/tree/HEAD/skills/refero-design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You design a landing page; You redesign a product screen; You polish a dashboard.
Skip it when: You only change backend code; You need print layout.

# Make it a habit: Designs grounded in real references.

When an issue gets the label design, your agent writes a brief, researches styles, screens and flows in Refero, locks one direction and builds it. The quality gate and a ledger check run before handoff. Past locks and ledgers stay in the loop folder.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** issue labelled design (event; GitHub Actions or Claude Code routine; `issues.labeled == design`)
- **Verification:** quality gate plus approval. Hard checks: reference lock is written before any code; every decision ledger row names a source; at least two full styles fetched with refero_get_style; rendered result compared against the locked reference. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** locks and ledgers at `loops/refero-design-loop/ledger.md`. Read first: earlier reference locks and decision ledgers.

## Steps

1. **Write the brief.** The agent drafts a short design brief and asks you only for facts that would change the result.
2. **Research styles.** It runs several refero_search_styles queries and fetches the strongest with refero_get_style.
3. **Screens and flows.** For concrete patterns it uses refero_search_screens, and for multi-step journeys refero_search_flows.
4. **Choose a direction.** For a big redesign it shows three reference-locked options and you pick one.
5. **Lock and ledger.** It writes the reference lock and a decision ledger where each choice has a source.
6. **Build.** It implements the design and keeps token and media roles from the references.
7. **Quality gate.** It runs the quality gate questions and compares the render with the lock, then fixes drift.

Stop rule: Stops after one design task and at most one retry.

## Permissions

- Writes: loops/refero-design-loop/**
- Network: api.refero.design
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/refero-design-loop/ledger.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: issue labelled design. Verification: quality gate plus approval. Memory: loops/refero-design-loop/ledger.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
