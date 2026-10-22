---
name: unslop
title: Unslop skill
repo: backnotprop/pstack
license: MIT
url: https://gethabit.dev/skills/backnotprop/unslop
---

# Unslop skill

The unslop skill edits any text to remove AI writing patterns: AI vocabulary, em dashes, inline-header lists, chatbot phrases, filler, jargon nouns, passive voice and over-compression, with stable rule ids. For anyone polishing docs or copy.

- Install the skill: `npx skills add backnotprop/pstack --skill unslop`
- Source: https://github.com/backnotprop/pstack/tree/HEAD/skills/unslop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You edit AI-written docs; You want plainer README text; You review copy for AI tells.
Skip it when: You write fiction with a set style; The text is code only.

# Make it a habit: Strip AI tells from new docs.

When docs or README text changes, your agent scans the new text for the numbered unslop patterns, from AI vocabulary and em dashes to passive voice and over-compression, rewrites while keeping meaning and tone, and logs which rule ids fired.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** docs text changes (event; GitHub Actions or Claude Code routine; `pull request touches .md or docs files`)
- **Verification:** pattern scan is clean. Hard checks: no em dashes in rewritten text; no words from the rule 7 vocabulary list; no curly quotes; headings use sentence case. On fail: retry, max 1 retries.
- **Memory:** rule hit log at `loops/unslop-docs-loop/hits.md`. Read first: rule ids that fired most often.

## Steps

1. **Scan content.** Your agent looks for superficial -ing phrases and vague attributions.
2. **Scan language.** It checks AI vocabulary, fancy ways to say is, rule of three and false ranges.
3. **Scan style.** It checks em dashes, colons, bold, inline-header lists, title case, emojis and curly quotes.
4. **Scan plain speech.** It checks jargon nouns, passive voice, adverbs, mannered prose and over-compression.
5. **Rewrite.** It rewrites flagged sentences, keeping meaning and tone, and logs the rule ids.

Stop rule: Stops after 20 files or one retry per run.

## Permissions

- Writes: docs/**, README.md, loops/unslop-docs-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/unslop-docs-loop/hits.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: docs text changes. Verification: pattern scan is clean. Memory: loops/unslop-docs-loop/hits.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
