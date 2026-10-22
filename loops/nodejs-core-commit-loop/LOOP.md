---
name: nodejs-core
title: Node.js Core skill
repo: mcollina/skills
license: MIT
url: https://gethabit.dev/skills/mcollina/nodejs-core
---

# Node.js Core skill

Node.js core is a skill for people who contribute to or debug nodejs/node: commit and PR style, the build-lint-test cycle, native addon crashes, V8 deoptimizations, node-gyp builds and libuv issues.

- Install the skill: `npx skills add mcollina/skills --skill nodejs-core`
- Source: https://github.com/mcollina/skills/tree/HEAD/skills/nodejs-core
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You commit to nodejs/node; A native addon segfaults; A function deoptimizes in V8.
Skip it when: You write normal app code in Node.js; You only need JavaScript help.

# Make it a habit: Commits that pass CI first.

Before each commit in a nodejs/node checkout, your agent rebuilds, runs make lint, formats C++ from the merge base, signs off and validates the message with core-validate-commit. It keeps your build setup for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** before each commit (event; Claude Code; `event: change to src/ or lib/ ready to commit`)
- **Verification:** lint and commit validation. Hard checks: make -j$(nproc) builds; make lint passes; git --no-pager diff --exit-code is empty after make format-cpp; npx core-validate-commit --no-validate-metadata HEAD passes. On fail: retry, max 2 retries.
- **Memory:** build setup notes at `loops/nodejs-core-commit-loop/notes.md`. Read first: your build configuration: Make or Ninja, debug or release, configure flags.

## Steps

1. **Ask build setup.** Ask the user about Make or Ninja, debug or release and configure flags, unless the notes already hold them.
2. **Rebuild.** Run make -j$(nproc) after any change to src/ or lib/ before testing.
3. **Lint.** Run make lint, and for C++ changes run make format-cpp with CLANG_FORMAT_START set to the merge base.
4. **Check the diff.** Run git --no-pager diff --exit-code and require it to be empty.
5. **Commit signed.** Commit with git commit -s using the human contributor's sign-off and a terse subsystem-prefixed title.
6. **Validate message.** Run npx core-validate-commit --no-validate-metadata HEAD and never add PR-URL or Reviewed-By.

Stop rule: Stops after one commit or two failed retries.

## Permissions

- Writes: src/**, lib/**, loops/nodejs-core-commit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nodejs-core-commit-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: before each commit. Verification: lint and commit validation. Memory: loops/nodejs-core-commit-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
