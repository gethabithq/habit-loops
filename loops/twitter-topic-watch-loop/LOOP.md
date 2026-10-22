---
name: twitter
title: Twitter/X skill
repo: resciencelab/opc-skills
license: Apache-2.0
url: https://gethabit.dev/skills/resciencelab/twitter
---

# Twitter/X skill

The twitter/x skill helps agents search and read Twitter/X content via twitterapi.io: user profiles, tweets, replies, followers, communities, spaces and trends.

- Install the skill: `npx skills add resciencelab/opc-skills --skill twitter`
- Source: https://github.com/resciencelab/opc-skills/tree/HEAD/skills/twitter
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You search tweets on a topic; You look up a user's recent posts; You check trends.
Skip it when: You want to post or reply; You have no twitterapi.io key.

# Make it a habit: Daily digest of your X topics.

Each day your agent runs search_tweets.py for each watched topic with --type Latest and a limit, filters out retweets, and writes a short digest of new posts. A log keeps tweet IDs already seen.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily topic search (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** searches return results. Hard checks: TWITTERAPI_API_KEY is set; each search_tweets.py call exits without error; count of new tweets in the digest is above zero or marked none. On fail: notify, max 1 retries.
- **Memory:** seen tweets log at `loops/twitter-topic-watch-loop/run-log.md`. Read first: tweet IDs already included in earlier digests.

## Steps

1. **Check the key.** Confirm TWITTERAPI_API_KEY is set.
2. **Search topics.** Run scripts/search_tweets.py with -filter:retweets, --type Latest and --limit 20 per topic.
3. **Drop seen posts.** Skip tweet IDs already in the log.
4. **Add threads.** Run scripts/get_tweet_thread.py for the most relevant new posts.
5. **Write digest.** Write the digest and log the new IDs.

Stop rule: Stops after 5 topics and 20 tweets per topic per run.

## Permissions

- Writes: loops/twitter-topic-watch-loop/**
- Network: api.twitterapi.io
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/twitter-topic-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily topic search. Verification: searches return results. Memory: loops/twitter-topic-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
