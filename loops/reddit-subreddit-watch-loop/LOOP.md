---
name: reddit
title: Reddit skill
repo: resciencelab/opc-skills
license: Apache-2.0
url: https://gethabit.dev/skills/resciencelab/reddit
---

# Reddit skill

The reddit skill searches and retrieves posts, comments, subreddit info and user profiles through Reddit's public JSON API, no API key needed. For people monitoring subreddits or researching discussions.

- Install the skill: `npx skills add resciencelab/opc-skills --skill reddit`
- Source: https://github.com/resciencelab/opc-skills/tree/HEAD/skills/reddit
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: pulling posts from a subreddit; searching Reddit for a topic; reading a thread's comments.
Skip it when: you need to post or vote, not read; the content is not on Reddit.

# Make it a habit: A daily pull of subreddit activity.

On a schedule, your agent pulls new and top posts, searches and subreddit info from Reddit's public JSON API for your tracked subreddits and queries. A run log keeps the last post ids seen.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily subreddit check (schedule; cron; `0 7 * * *`)
- **Verification:** posts returned. Hard checks: get_posts.py returns posts for a subreddit, count above zero; a search returns results when a query is set; the record file is written. On fail: notify, max 1 retries.
- **Memory:** subreddit log at `loops/reddit-subreddit-watch-loop/run-log.md`. Read first: the last post ids seen per subreddit and query.

## Steps

1. **Load watchlist.** Your agent reads the subreddits, queries and sort options to pull.
2. **Pull posts.** It runs get_posts.py for each subreddit with the chosen sort and limit.
3. **Search.** It runs search_posts.py for your tracked queries, scoped to a subreddit when set.
4. **Fetch details.** It pulls a post and its comments with get_post.py when a thread matters.
5. **Record.** It writes the new posts and the last ids to the run log.

Stop rule: Stops after one pass over the watchlist per run, within the 100 requests per minute limit.

## Permissions

- Writes: loops/reddit-subreddit-watch-loop/**
- Network: reddit.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/reddit-subreddit-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily subreddit check. Verification: posts returned. Memory: loops/reddit-subreddit-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
