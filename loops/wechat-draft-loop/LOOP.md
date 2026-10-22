---
name: baoyu-post-to-wechat
title: Baoyu Post to WeChat skill
repo: JimLiu/baoyu-skills
license: MIT
url: https://gethabit.dev/skills/jimliu/baoyu-post-to-wechat
---

# Baoyu Post to WeChat skill

The baoyu post to wechat skill posts articles and image posts to a WeChat Official Account through the API, a browser or a remote API host, with themes and auto metadata. For creators who publish on WeChat.

- Install the skill: `npx skills add JimLiu/baoyu-skills --skill baoyu-post-to-wechat`
- Source: https://github.com/JimLiu/baoyu-skills/tree/HEAD/skills/baoyu-post-to-wechat
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You post articles to a WeChat Official Account; You turn Markdown into a WeChat draft; You manage several accounts.
Skip it when: You do not have a WeChat Official Account; You post to other platforms.

# Make it a habit: Finished posts land as drafts.

When a Markdown article is marked ready, your agent loads EXTEND.md, checks title, summary, author and cover, and saves it as a WeChat Official Account draft with wechat-api.ts. You publish from the draft box. A log keeps media IDs.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** article marked ready (event; Claude Code routine; `new .md file in the ready folder`)
- **Verification:** draft saved + you. Hard checks: wechat-api.ts returns a media_id; a cover image is found before upload; title and summary are set. On fail: notify, max 1 retries.
- **Memory:** draft log at `loops/wechat-draft-loop/drafts.md`. Read first: articles already sent as drafts.

## Steps

1. **Load preferences.** Read EXTEND.md, or run first-time setup if it is missing.
2. **Pick the account.** Ask which account to use when EXTEND.md lists more than one.
3. **Check input.** Detect HTML, Markdown or plain text, and save plain text as Markdown.
4. **Choose method.** Use api, browser or remote-api from EXTEND.md, or ask you.
5. **Fill metadata.** Resolve theme, title, summary, author and cover, and ask for missing ones.
6. **Save the draft.** Run wechat-api.ts with --theme and without converting Markdown first.
7. **Report.** Show the completion report with the media_id and the draft box link.

Stop rule: Stops after one article per run.

## Permissions

- Writes: post-to-wechat/**, .baoyu-skills/.env, loops/wechat-draft-loop/**
- Network: api.weixin.qq.com
- Sends: draft to the WeChat Official Account
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/wechat-draft-loop/drafts.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: article marked ready. Verification: draft saved + you. Memory: loops/wechat-draft-loop/drafts.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
