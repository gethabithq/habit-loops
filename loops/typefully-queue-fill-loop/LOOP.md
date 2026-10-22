---
name: typefully
title: Typefully skill
repo: typefully/agent-skills
license: MIT
url: https://gethabit.dev/skills/typefully/typefully
---

# Typefully skill

The typefully skill helps creators draft, schedule and publish posts on X, LinkedIn, Threads, Bluesky, Mastodon and Substack Notes through the Typefully CLI script.

- Install the skill: `npx skills add typefully/agent-skills --skill typefully`
- Source: https://github.com/typefully/agent-skills/tree/HEAD/skills/typefully
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You draft a thread or post; You check what is scheduled; You post one draft to several platforms.
Skip it when: You have no Typefully account; You want automated replies.

# Make it a habit: Next week's social queue drafted.

Each week your agent checks free slots with queue:get, drafts posts as single multi-platform drafts with ./scripts/typefully.js, plans them into free slots without auto-publishing, and asks you before scheduling or publishing anything.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly queue fill (schedule; Claude Code routine; `0 10 * * 5`)
- **Verification:** drafts within limits, approved. Hard checks: every X post is 280 characters or fewer; each post is one draft covering its platforms; no draft is scheduled or published without your OK. On fail: stop, max 0 retries.
- **Memory:** queue fill log at `loops/typefully-queue-fill-loop/run-log.md`. Read first: drafts planned last week and their status.

## Steps

1. **Pick the account.** Run config:show, then social-sets:list if no default is set.
2. **Read the queue.** Run queue:get for next week to see free slots and planned drafts.
3. **Draft posts.** Create one draft per post with drafts:create and --platform, splitting threads with ---.
4. **Plan, not publish.** Use --plan next-free-slot so drafts sit dated but inert.
5. **Confirm with you.** Ask before confirming any draft with drafts:schedule or drafts:publish.

Stop rule: Stops after 10 drafts per run.

## Permissions

- Writes: loops/typefully-queue-fill-loop/**
- Network: typefully.com
- Sends: Typefully drafts:schedule, Typefully drafts:publish
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/typefully-queue-fill-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly queue fill. Verification: drafts within limits, approved. Memory: loops/typefully-queue-fill-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
