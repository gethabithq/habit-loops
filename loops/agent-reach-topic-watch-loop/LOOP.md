---
name: skill
title: Agent Reach skill
repo: panniantong/agent-reach
license: MIT
url: https://gethabit.dev/skills/panniantong/skill
---

# Agent Reach skill

Agent reach routes an agent's internet research across 16 platforms, including web search, Twitter, Reddit, Xiaohongshu, Bilibili, YouTube, GitHub and RSS, with one health check per backend. For people who research topics across Chinese and global platforms.

- Install the skill: `npx skills add panniantong/agent-reach --skill skill`
- Source: https://github.com/panniantong/agent-reach/tree/HEAD/agent_reach/skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You research a topic across platforms; You read a link from social media; You want YouTube or Bilibili subtitles.
Skip it when: You want to post or comment; A platform already has its own skill.

# Make it a habit: Fresh cross-platform research, read-only.

Each morning your agent runs agent-reach doctor, then searches the web, Twitter, Reddit, Bilibili and other channels for your watched topics, read-only. It keeps only results with real content and logs what it already reported so the next run shows only new items.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily topic scan (schedule; Claude Code routine; `0 8 * * *`)
- **Verification:** doctor + non-empty results. Hard checks: agent-reach doctor --json returns a backend list; each kept result has non-empty content; the run stops at once on ENVIRONMENT_RISK. On fail: notify, max 1 retries.
- **Memory:** reported items log at `loops/agent-reach-topic-watch-loop/log.md`. Read first: watched topics and the links already reported.

## Steps

1. **Read the log.** Load the watched topics and the links reported in earlier runs.
2. **Run the health check.** Run agent-reach doctor --json and pick each platform's command group from active_backend.
3. **Search in parallel.** Combine Exa web search with Twitter, Reddit, Xiaohongshu and Bilibili searches for each topic.
4. **Read the sources.** Open promising links with the Jina reader or yt-dlp subtitles, following the retry chains in the references.
5. **Keep new content.** Drop empty results and links already in the log, then write a short digest.
6. **Check for updates.** Run agent-reach check-update and mention a new version once in the digest.

Stop rule: Stops after at most 5 topics and 10 results per topic per run.

## Permissions

- Writes: /tmp/**, ~/.agent-reach/**, loops/agent-reach-topic-watch-loop/**
- Network: r.jina.ai, www.v2ex.com, raw.githubusercontent.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agent-reach-topic-watch-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily topic scan. Verification: doctor + non-empty results. Memory: loops/agent-reach-topic-watch-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
