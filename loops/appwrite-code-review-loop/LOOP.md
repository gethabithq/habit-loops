---
name: appwrite-typescript
title: Appwrite TypeScript skill
repo: appwrite/skills
license: BSD-3-Clause
url: https://gethabit.dev/skills/appwrite/appwrite-typescript
---

# Appwrite TypeScript skill

The appwrite typescript skill helps web, React Native and Node.js developers use the Appwrite SDK for auth, TablesDB queries, storage, realtime, functions and SSR sessions.

- Install the skill: `npx skills add appwrite/skills --skill appwrite-typescript`
- Source: https://github.com/appwrite/skills/tree/HEAD/skills/appwrite-typescript
- Licence: BSD-3-Clause (Habit links to this skill and does not host or change it)

Use it when: You build an app on Appwrite; You set up OAuth in React Native; You write TablesDB queries.
Skip it when: You use another backend service; You write Appwrite code in another language.

# Make it a habit: Appwrite code follows current SDK patterns.

On each pull request that touches Appwrite code, your agent checks for the deprecated Databases class and legacy string columns, risky Role.any() permissions, missing row permissions, React Native OAuth misuse and unsafe session cookies, then reports fixes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Appwrite code changed (event; Claude Code routine or GitHub Actions; `a pull request changes files importing appwrite or node-appwrite`)
- **Verification:** tests pass, patterns clean. Hard checks: tests pass; no new code uses the Databases class; no Role.any() is paired with write, update or delete; session cookies set httpOnly, secure and sameSite strict. On fail: notify, max 1 retries.
- **Memory:** review findings log at `loops/appwrite-code-review-loop/run-log.md`. Read first: patterns flagged in earlier reviews.

## Steps

1. **Find SDK use.** List changed files that import appwrite, react-native-appwrite or node-appwrite.
2. **Check APIs.** Flag Databases instead of TablesDB and positional instead of object params.
3. **Check columns.** Flag the legacy string type in favor of varchar, text, mediumtext or longtext.
4. **Check permissions.** Flag Role.any() with write, update or delete and rows without permissions.
5. **Check auth.** Flag createOAuth2Session on React Native and weak a_session_ cookies.
6. **Report.** Post findings with the matching fix from the skill.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/appwrite-code-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/appwrite-code-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Appwrite code changed. Verification: tests pass, patterns clean. Memory: loops/appwrite-code-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
