---
name: durable-objects
title: Durable Objects skill
repo: cloudflare/skills
license: Apache-2.0
url: https://gethabit.dev/skills/cloudflare/durable-objects
---

# Durable Objects skill

The durable objects skill helps agents build, debug and review Cloudflare Durable Objects code for persistent state and coordination, with current docs, wrangler config, storage, alarms and Vitest testing. For Workers developers.

- Install the skill: `npx skills add cloudflare/skills --skill durable-objects`
- Source: https://github.com/cloudflare/skills/tree/HEAD/skills/durable-objects
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build chat rooms, games or per-user state; You configure DO bindings and migrations; You review existing DO code.
Skip it when: Your requests are stateless; You need high fan-out independent requests.

# Make it a habit: Durable Object code stays safe.

When a pull request touches Durable Object code or wrangler.jsonc, your agent fetches the current Cloudflare docs, reviews the change against the critical rules and anti-patterns, and runs the Vitest suite. A board keeps open findings for the next review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches Durable Objects (event; GitHub Actions or Claude Code routine; `pull_request paths: wrangler.jsonc, wrangler.toml, files extending DurableObject`)
- **Verification:** Vitest plus rule check. Hard checks: Vitest suite passes; new classes are listed in new_sqlite_classes migrations; no blockConcurrencyWhile() call inside a per-request path. On fail: notify, max 0 retries.
- **Memory:** open DO findings at `loops/durable-objects-review-loop/board.md`. Read first: findings still open from earlier reviews.

## Steps

1. **Fetch current docs.** Pull the Durable Objects docs, API reference and best practices pages instead of relying on old knowledge.
2. **Read the references.** Check the change against references/rules.md, references/workers.md and references/testing.md.
3. **Check the rules.** Look for one DO per coordination atom, getByName() routing, SQLite storage, persist-first writes and one alarm per DO.
4. **Flag anti-patterns.** Flag a single global DO, state kept only in memory, and await between related storage writes.
5. **Run the tests.** Run the Vitest suite with the Cloudflare integration and record the result.
6. **Update the board.** Write new findings to the board and close the ones the change fixed.

Stop rule: One pull request per run, no retries.

## Permissions

- Writes: loops/durable-objects-review-loop/**
- Network: developers.cloudflare.com, api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/durable-objects-review-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches Durable Objects. Verification: Vitest plus rule check. Memory: loops/durable-objects-review-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
