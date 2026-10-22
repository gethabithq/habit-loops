---
name: copywriting
title: Copywriting skill
repo: coreyhaines31/marketingskills
license: MIT
url: https://gethabit.dev/skills/coreyhaines31/copywriting
---

# Copywriting skill

The copywriting skill has your agent write or fix marketing copy for homepages, landing, pricing and feature pages, with no AI tells and only claims it can support. For founders and marketers who want copy that sounds human.

- Install the skill: `npx skills add coreyhaines31/marketingskills --skill copywriting`
- Source: https://github.com/coreyhaines31/marketingskills/tree/HEAD/skills/copywriting
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you need a new landing page; your copy sounds like AI; a headline or CTA is weak.
Skip it when: you write emails or popups; you only need proofreading.

# Make it a habit: Clear copy without AI tells.

When a page needs copy, your agent reads your product marketing file and its learnings log, then drafts unit by unit. Every line passes the three-question gate and the AI-tell check. After your OK, the chosen angle and declined claims go into the log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** copy brief opened (event; GitHub Actions or Claude Code routine; `issue labelled copy`)
- **Verification:** AI-tell scan + your OK. Hard checks: no it's-not-X-it's-Y reveals in the draft; no no-X-no-Y-no-Z negation lists; no em dashes in headlines or subheads; no exclamation points; every unsupported claim carries a [NEED: ...] flag; the diagnosis line states A, B or C. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** copy learnings log at `loops/copywriting-loop/learnings.md`. Read first: angles already used, declined claims with their unlock evidence, and the Learnings in .agents/product-marketing.md.

## Steps

1. **Read the context.** Read .agents/product-marketing.md with its Learnings section and the learnings log, then ask only for what is missing.
2. **Diagnose first.** Decide if this is a blank brief, a draft with real voice, or a point edit, and say why.
3. **Draft by unit.** Write two or three candidates for each headline, CTA and section, keep the best and lock it.
4. **Run the gate.** Check each line: can the reader picture it, can it be proven, could a competitor say it.
5. **Remove AI tells.** Scan for banned patterns, read long sentences and flag missing proof with [NEED: ...].
6. **Hand over.** Save page copy with notes and two or three headline and CTA options to drafts/, and ask for your approval.
7. **Log the learnings.** After your OK, add the chosen angle, declined claims and the evidence that would unlock them to the learnings log.

Stop rule: Stops after one page per run and one rewrite pass.

## Permissions

- Writes: loops/copywriting-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/copywriting-loop/learnings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: copy brief opened. Verification: AI-tell scan + your OK. Memory: loops/copywriting-loop/learnings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
