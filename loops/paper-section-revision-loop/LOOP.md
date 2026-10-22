---
name: research-paper-writing
title: Research Paper Writing skill
repo: master-cai/research-paper-writing-skills
license: MIT
url: https://gethabit.dev/skills/master-cai/research-paper-writing
---

# Research Paper Writing skill

The research paper writing skill helps ML, CV and NLP researchers draft and revise papers with clear sections, one-message paragraphs, claim-evidence checks and a reviewer-style self-review.

- Install the skill: `npx skills add master-cai/research-paper-writing-skills --skill research-paper-writing`
- Source: https://github.com/master-cai/research-paper-writing-skills/tree/HEAD/research-paper-writing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You revise an Introduction or Method section; You check claims against results; You self-review before submission.
Skip it when: You need experiments run; You write a non-academic text.

# Make it a habit: One paper section clearer each pass.

Each writing session your agent takes the next section, loads only its guide, outlines it, rewrites paragraph by paragraph with one message each, runs reverse outlining and builds a claim-evidence map. A board tracks sections and open claims.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** next section to revise (manual; Claude Code routine; `run when you pick the next paper section`)
- **Verification:** claims mapped, review done. Hard checks: every major claim has a Claim | Evidence | Status line; no claim marked needs evidence remains in Abstract or Introduction; the five-dimension self-review list is answered. On fail: retry, max 1 retries.
- **Memory:** section revision board at `loops/paper-section-revision-loop/board.md`. Read first: sections revised, terminology list and claims needing evidence.

## Steps

1. **Clarify the story.** State the paper's story before sentence edits.
2. **Load one guide.** Load only the guide for the section, such as references/method.md.
3. **Outline.** Write a 3 to 7 bullet outline for the section.
4. **Rewrite.** Rewrite each paragraph with one message stated in its first sentence.
5. **Reverse outline.** Map topic sentences to the thesis and fix paragraphs that do not map.
6. **Map claims.** Build the claim-evidence map and weaken unsupported claims.
7. **Self-review.** Before submission, run references/paper-review.md as a skeptical reviewer.

Stop rule: Stops after one section per run.

## Permissions

- Writes: loops/paper-section-revision-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/paper-section-revision-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: next section to revise. Verification: claims mapped, review done. Memory: loops/paper-section-revision-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
