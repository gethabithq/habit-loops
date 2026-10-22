---
name: mintlify
title: Mintlify skill
repo: mintlify/docs
license: MIT
url: https://gethabit.dev/skills/mintlify/mintlify
---

# Mintlify skill

The mintlify skill helps agents set up, write and publish documentation sites with Mintlify: docs.json, navigation, components, API references from OpenAPI, migration from other platforms and local preview. For teams who ship product docs.

- Install the skill: `npx skills add mintlify/docs --skill mintlify`
- Source: https://github.com/mintlify/docs/tree/HEAD/agent-context/context/skills/mintlify
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You turn a docs folder or README into a docs site; You document an API from an OpenAPI spec; You migrate from Docusaurus or GitBook.
Skip it when: You use a different docs platform; You only need a single README.

# Make it a habit: Docs pages that validate cleanly.

When a pull request changes Mintlify docs, your agent reads docs.json, runs mint validate and mint broken-links, checks code block language tags, alt text and navigation, fixes what it caused, and publishes only when you ask.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes docs (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.mdx, docs.json`)
- **Verification:** validate passes + your OK. Hard checks: mint validate passes; mint broken-links finds no broken links; every code block has a language tag; every image has alt text; every new page is in docs.json navigation. On fail: retry, max 2 retries.
- **Memory:** product brief at `.mintlify/product-brief.md`. Read first: the product brief and docs.json.

## Steps

1. **Read the context.** The agent reads docs.json and .mintlify/product-brief.md, and 2-3 similar pages for voice.
2. **Check the pages.** It checks frontmatter, root-relative links without extensions, language tags and alt text.
3. **Check navigation.** It confirms every new page is listed in docs.json.
4. **Run the CLI.** It runs mint validate, mint broken-links and mint a11y and fixes issues it caused.
5. **Preview.** It runs mint dev --no-open and reports the local URL.
6. **Publish on request.** You decide when to publish; the agent pushes or calls publish only after you ask.

Stop rule: Stops after one pull request and at most 2 fix retries.

## Permissions

- Writes: **/*.mdx, docs.json, images/**, loops/mintlify-docs-check-loop/**
- Network: mintlify.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.mintlify/product-brief.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes docs. Verification: validate passes + your OK. Memory: .mintlify/product-brief.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
