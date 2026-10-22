---
name: huggingface-papers
title: Hugging Face Paper Pages skill
repo: huggingface/skills
license: Apache-2.0
url: https://gethabit.dev/skills/huggingface/huggingface-papers
---

# Hugging Face Paper Pages skill

The hugging face paper pages skill reads AI research papers as markdown and pulls structured metadata such as linked models, datasets, spaces and GitHub repos, for anyone summarizing or tracking papers.

- Install the skill: `npx skills add huggingface/skills --skill huggingface-papers`
- Source: https://github.com/huggingface/skills/tree/HEAD/skills/huggingface-papers
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: someone shares an arXiv link; you want a paper summarized; you track the daily papers feed.
Skip it when: the paper is outside AI or CS; you need full PDF figure extraction.

# Make it a habit: Never miss an important paper.

Every weekday your agent pulls the Hugging Face Daily Papers feed, reads the top papers as markdown, and lists linked models, datasets and spaces. It keeps a digest log so papers already covered are skipped next time.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekday morning digest (schedule; Claude Code routine or cron; `0 8 * * 1-5`)
- **Verification:** feed fetched, papers summarized. Hard checks: daily_papers request returns a list; count of new papers above zero or noted as none; every summary carries its paper ID; no paper from the log repeated. On fail: retry, max 1 retries.
- **Memory:** paper digest log at `loops/daily-papers-digest-loop/digest.md`. Read first: paper IDs already summarized.

## Steps

1. **Fetch the feed.** The agent calls /api/daily_papers for today with sort set to trending.
2. **Skip known papers.** It drops paper IDs already in the digest log.
3. **Read each paper.** It fetches each paper as markdown from the .md endpoint, falling back to arXiv when needed.
4. **Add linked work.** It queries linked models, datasets and spaces with the arxiv filter.
5. **Write the digest.** Short summaries with paper IDs and links go into the digest log.

Stop rule: Stops after 10 papers per run.

## Permissions

- Writes: loops/daily-papers-digest-loop/**
- Network: huggingface.co, arxiv.org
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/daily-papers-digest-loop/digest.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekday morning digest. Verification: feed fetched, papers summarized. Memory: loops/daily-papers-digest-loop/digest.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
