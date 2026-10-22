---
name: knowledge-agent
title: Knowledge Agent skill
repo: thedotmack/claude-mem
license: Apache-2.0
url: https://gethabit.dev/skills/thedotmack/knowledge-agent
---

# Knowledge Agent skill

The knowledge agent skill lets claude-mem users build focused knowledge bases from their observation history, prime them into an AI session and ask questions about past work, decisions and bugfixes.

- Install the skill: `npx skills add thedotmack/claude-mem --skill knowledge-agent`
- Source: https://github.com/thedotmack/claude-mem/tree/HEAD/plugin/skills/knowledge-agent
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You use claude-mem; You ask about past decisions; You collect expertise on a topic.
Skip it when: You do not use claude-mem; You need facts from outside your work history.

# Make it a habit: Keep your work brains current.

Every week your agent rebuilds each claude-mem knowledge corpus with new observations, reprimes it and asks it a fixed set of questions. It checks that the corpus is primed and answers, and keeps the answers for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** corpus primed and answering. Hard checks: list_corpora shows each corpus as primed; each corpus holds more than zero observations; query_corpus returns an answer for every standing question. On fail: retry, max 1 retries.
- **Memory:** weekly brain answers at `loops/knowledge-brain-refresh-loop/answers.md`. Read first: the standing questions and last week's answers per corpus.

## Steps

1. **List corpora.** list_corpora shows every corpus with its stats and priming status.
2. **Rebuild.** rebuild_corpus pulls the newest observations into each corpus.
3. **Reprime.** reprime_corpus loads the updated knowledge into a fresh session.
4. **Ask.** query_corpus asks each corpus the standing questions from the answers file.
5. **Compare.** The agent notes where an answer changed since last week.
6. **Save.** The new answers and changes go into the answers file.

Stop rule: Stops after all listed corpora, at most one retry per corpus.

## Permissions

- Writes: loops/knowledge-brain-refresh-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/knowledge-brain-refresh-loop/answers.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: corpus primed and answering. Memory: loops/knowledge-brain-refresh-loop/answers.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
