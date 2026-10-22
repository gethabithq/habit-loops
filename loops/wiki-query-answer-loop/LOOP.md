---
name: wiki-query
title: Wiki Query skill
repo: ar9av/obsidian-wiki
license: MIT
url: https://gethabit.dev/skills/ar9av/wiki-query
---

# Wiki Query skill

Wiki Query answers questions from a compiled Obsidian wiki with cited, multi-hop answers, a graph pre-pass and optional semantic search, and it stays read-only. For people who keep an LLM-maintained Obsidian wiki.

- Install the skill: `npx skills add ar9av/obsidian-wiki --skill wiki-query`
- Source: https://github.com/ar9av/obsidian-wiki/tree/HEAD/.skills/wiki-query
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: answering from existing wiki knowledge; a fast index-only lookup; challenging a plan with your own notes.
Skip it when: you want to add or edit pages; you have no compiled wiki yet.

# Make it a habit: Cited answers from your own wiki.

On a question, your agent searches the compiled Obsidian wiki cheapest-first: graph pre-pass, index, optional semantic search, then full reads, and answers with cited pages. It logs each query to the vault's log.md and writes nothing else.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you ask a question (manual; Claude Code routine; `run wiki-query on demand`)
- **Verification:** answer cites pages. Hard checks: the answer cites specific wiki pages or says the wiki does not cover it; the retrieval line reports candidates seen, used and dropped; the query is logged with obsidian-wiki memory log QUERY. On fail: notify, max 0 retries.
- **Memory:** wiki query log at `log.md`. Read first: hot.md and index.md for recent activity and the wiki's scope.

## Steps

1. **Resolve config.** Your agent resolves the vault path and QMD settings, then reads hot.md and index.md.
2. **Graph pre-pass.** It runs graph-query first; a structural answer is reported straight from the graph with no page reads.
3. **Index pass.** It greps frontmatter for title, tag and summary matches to build a small candidate set.
4. **Semantic pass.** If a QMD collection is set it runs a semantic search, dropping any _raw/ paths.
5. **Section and full read.** It reads only the sections or top pages it needs, following at most one wikilink hop.
6. **Synthesize.** It answers with cited pages, flags stale or disputed pages, and names gaps.
7. **Log.** It appends one query line to log.md and changes nothing else.

Stop rule: Stops after one question per run; this skill is read-only and never retries into writes.

## Permissions

- Writes: log.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you ask a question. Verification: answer cites pages. Memory: log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
