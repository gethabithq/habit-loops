---
name: review-pr
title: Review PR skill
repo: warpdotdev/common-skills
license: MIT
url: https://gethabit.dev/skills/warpdotdev/review-pr
---

# Review PR skill

The review pr skill reviews a checked-out pull request from pr_diff.txt and writes labelled, line-exact findings to review.json for a CI workflow to publish, checked by a bundled validator.

- Install the skill: `npx skills add warpdotdev/common-skills --skill review-pr`
- Source: https://github.com/warpdotdev/common-skills/tree/HEAD/.agents/skills/review-pr
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You run PR reviews in CI; You need machine-readable review output; You want suggestion blocks on exact lines.
Skip it when: You want the agent to post comments directly; There is no annotated diff file.

# Make it a habit: Every PR gets a validated review.

On each pull request, your agent reads pr_diff.txt and pr_description.txt, audits every changed comment and test, and writes labelled findings to review.json. The bundled validator must pass before the workflow publishes it. Past verdicts are kept in a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions; `pull_request.opened, pull_request.synchronize`)
- **Verification:** validator passes. Hard checks: validate_review_json.py passes against pr_diff.txt; review.json is valid JSON with verdict APPROVE or REJECT; verdict matches the recommendation in body; every inline comment points to an annotated diff line. On fail: retry, max 2 retries.
- **Memory:** verdicts per PR at `loops/pr-review-json-loop/run-log.md`. Read first: earlier verdicts and issue counts for this PR.

## Steps

1. **Load local guidance.** The agent looks for a review-pr-local companion skill and applies it if found.
2. **Read inputs.** It reads pr_diff.txt, pr_description.txt and spec_context.md when present.
3. **Add companion checks.** It applies security-review-pr and check-impl-against-spec when the repository provides them.
4. **Audit comments and tests.** It checks every changed comment and test one by one against repository conventions.
5. **Write review.json.** Findings get CRITICAL, IMPORTANT, SUGGESTION or NIT labels and exact diff lines.
6. **Validate.** It runs validate_review_json.py and fixes review.json until it passes.

Stop rule: One pull request per run, at most two validator retries.

## Permissions

- Writes: review.json, loops/pr-review-json-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pr-review-json-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: validator passes. Memory: loops/pr-review-json-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
