---
name: read-deleted-pages
title: Read Deleted Pages skill
repo: useosint/skills
license: MIT
url: https://gethabit.dev/skills/useosint/read-deleted-pages
---

# Read Deleted Pages skill

The read deleted pages skill helps investigators, journalists and diligence teams recover deleted or edited web pages with the Wayback CDX API, archive.today and Common Crawl, and preserve evidence.

- Install the skill: `npx skills add useosint/skills --skill read-deleted-pages`
- Source: https://github.com/useosint/skills/tree/HEAD/skills/read-deleted-pages
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A page now returns 404; You need what a site said before; You must preserve web evidence.
Skip it when: The content is behind a login; You plan to republish erased personal data.

# Make it a habit: Watched page changes preserved as evidence.

Each week your agent queries the Wayback CDX API with collapse=digest for each watched URL, fetches new versions raw with id_, diffs them as text, submits the live page to Save Page Now and archive.today and keeps a hashed WARC copy.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly archive check (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** captures hashed and logged. Hard checks: each new capture has statuscode 200 and a digest in the CDX index; a WARC file and its sha256sum file exist per preserved page; every citation has the archive URL, timestamp and UTC capture time. On fail: notify, max 1 retries.
- **Memory:** watched URLs and digests at `loops/page-change-archive-loop/watchlist.md`. Read first: the last digest seen per URL.

## Steps

1. **Query CDX.** Run the CDX query with output=json and collapse=digest for each watched URL.
2. **Fetch raw.** Download new captures with the id_ suffix, not the replay page.
3. **Diff.** Compare raw captures as text and note what was removed.
4. **Preserve live.** Submit the URL to Save Page Now and archive.today.
5. **Keep your copy.** Save a WARC with wget --warc-file and hash it with sha256sum.
6. **Grade.** Grade each finding as confirmed, probable, unconfirmed or rejected.

Stop rule: Stops after 20 watched URLs per run.

## Permissions

- Writes: loops/page-change-archive-loop/**
- Network: web.archive.org, archive.today
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/page-change-archive-loop/watchlist.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly archive check. Verification: captures hashed and logged. Memory: loops/page-change-archive-loop/watchlist.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
