---
name: rust-skills
title: Rust Skills skill
repo: leonardomso/rust-skills
license: MIT
url: https://gethabit.dev/skills/leonardomso/rust-skills
---

# Rust Skills skill

The rust skills skill gives 265 Rust coding rules in 26 categories, from ownership and error handling to async, unsafe, API design and performance, ranked by impact. For Rust developers who write or review code with an agent.

- Install the skill: `npx skills add leonardomso/rust-skills --skill rust-skills`
- Source: https://github.com/leonardomso/rust-skills
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write new Rust code; You review a Rust pull request; You tune Rust performance.
Skip it when: The project is not Rust; You only need a formatter.

# Make it a habit: Keep Rust code idiomatic and safe.

On each pull request your agent maps changed Rust code to rule categories, checks CRITICAL ones first such as ownership, errors, memory and unsafe, fixes findings and runs clippy, rustfmt and tests. A board keeps rule ids that keep failing.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Rust pull request opened (event; GitHub Actions or Claude Code routine; `pull request touches .rs files`)
- **Verification:** clippy, fmt and tests. Hard checks: cargo fmt --check passes; clippy reports no correctness errors; cargo test passes; every unsafe block has a SAFETY comment. On fail: retry, max 2 retries.
- **Memory:** repeat rule findings at `loops/rust-guidelines-review-loop/board.md`. Read first: rule ids flagged most often.

## Steps

1. **Map the task.** Your agent picks the rule prefixes for the change, such as own-, err- and async-.
2. **Check critical rules.** It checks CRITICAL categories first, then HIGH, then MEDIUM.
3. **Read rule files.** It opens the matching file in rules/ for examples when unsure.
4. **Check anti-patterns.** It scans for anti- rules like unwrap in production or locks across await.
5. **Fix and verify.** It fixes findings and runs cargo fmt --check, clippy and tests.

Stop rule: Stops after 20 files or 2 fix rounds per run.

## Permissions

- Writes: src/**, loops/rust-guidelines-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/rust-guidelines-review-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Rust pull request opened. Verification: clippy, fmt and tests. Memory: loops/rust-guidelines-review-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
