---
name: domain-modeling
title: Domain Modeling skill
repo: pandoscope/skills
license: MIT
url: https://gethabit.dev/skills/pandoscope/domain-modeling
---

# Domain Modeling skill

Domain modeling is a skill for teams that build a project's ubiquitous language: it challenges terms, sharpens fuzzy words, checks them against code and writes one glossary file per term in docs/glossary/.

- Install the skill: `npx skills add pandoscope/skills --skill domain-modeling`
- Source: https://github.com/pandoscope/skills/tree/HEAD/derived/domain-modeling
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Terms mean different things to the team; You define a ubiquitous language; You record an architecture decision.
Skip it when: You only read existing terms; You need a technical spec.

# Make it a habit: One clear term per concept.

During design sessions, your agent challenges terms against docs/glossary/, sharpens fuzzy words with you, checks claims against the code and writes each resolved term as its own glossary file. It lints the glossary after each edit.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start design session (manual; Claude Code; `manual: domain modeling session`)
- **Verification:** glossary lint passes. Hard checks: uvx disambiguate --lint passes; each glossary file starts with an H2 canonical name; filenames are unique lowercase slugs. On fail: retry, max 1 retries.
- **Memory:** project glossary at `docs/glossary/`. Read first: existing terms and their avoided synonyms.

## Steps

1. **Challenge terms.** Point out when the user's word conflicts with docs/glossary/.
2. **Sharpen language.** Ask the user to pick a precise term for vague or overloaded words.
3. **Test scenarios.** Invent edge-case scenarios that force clear concept boundaries.
4. **Check the code.** Compare the user's claims with the code and surface contradictions.
5. **Write the term.** Write the resolved term as its own file, using writing-prose if available.
6. **Offer ADRs.** Offer an ADR through writing-adrs only when its three-part bar is met.
7. **Lint.** Run uvx disambiguate --lint after editing.

Stop rule: Stops after ten resolved terms per session, with one lint retry.

## Permissions

- Writes: docs/glossary/**, docs/adr/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/glossary/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start design session. Verification: glossary lint passes. Memory: docs/glossary/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
