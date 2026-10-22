---
name: producthunt
title: ProductHunt skill
repo: resciencelab/opc-skills
license: Apache-2.0
url: https://gethabit.dev/skills/resciencelab/producthunt
---

# ProductHunt skill

The producthunt skill fetches posts, topics, users, comments and collections from Product Hunt through its official GraphQL API, for founders and marketers who track product launches.

- Install the skill: `npx skills add resciencelab/opc-skills --skill producthunt`
- Source: https://github.com/resciencelab/opc-skills/tree/HEAD/skills/producthunt
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You track launches in a topic; You research a competitor's launch; You want today's featured posts.
Skip it when: You need to post a launch; You have no developer token.

# Make it a habit: Daily digest of new launches.

Every morning your agent pulls the featured Product Hunt posts and the posts in your topics through the GraphQL API, skips posts it already saw and writes a short digest. A seen-list file keeps post IDs so the next run reports only new ones.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine or cron; `0 8 * * *`)
- **Verification:** digest has new posts. Hard checks: get_posts.py returns without error; digest file exists; count of new posts is above zero or the digest says none. On fail: notify, max 1 retries.
- **Memory:** seen post IDs at `loops/producthunt-watch-loop/seen.md`. Read first: post IDs already reported and watched topics.

## Steps

1. **Check the token.** Confirm PRODUCTHUNT_ACCESS_TOKEN is set with a quick get_posts.py --limit 3 call.
2. **Pull featured posts.** Run get_posts.py with a limit to fetch today's featured posts.
3. **Pull topic posts.** Run get_posts.py --topic for each watched topic.
4. **Drop seen posts.** Compare post IDs with the seen list and keep only new ones.
5. **Write the digest.** Summarize each new post in one line and save the digest.
6. **Update the list.** Add the new post IDs to the seen list.

Stop rule: Stops after 20 posts per topic per run.

## Permissions

- Writes: loops/producthunt-watch-loop/**
- Network: api.producthunt.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/producthunt-watch-loop/seen.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: digest has new posts. Memory: loops/producthunt-watch-loop/seen.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
