---
name: typescript-discriminated-unions
title: Discriminated Unions skill
repo: mkosir/typescript-style-guide
license: MIT
url: https://gethabit.dev/skills/mkosir/typescript-discriminated-unions
---

# Discriminated Unions skill

The typescript-discriminated-unions skill applies, reviews and explains discriminated unions in TypeScript to model mutually exclusive variants, prevent invalid states and enforce exhaustiveness. For TypeScript developers modelling state and props.

- Install the skill: `npx skills add mkosir/typescript-style-guide --skill typescript-discriminated-unions`
- Source: https://github.com/mkosir/typescript-style-guide/tree/HEAD/skills/typescript-discriminated-unions
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: modelling mutually exclusive variants; replacing boolean flags for app state; typing variant-specific props.
Skip it when: properties are independently optional; the project is not TypeScript.

# Make it a habit: Invalid states removed from the code.

When TypeScript changes, your agent reviews types for mutually exclusive variants hidden behind optional properties or boolean flags, suggests discriminated unions, and checks exhaustiveness and the build. A run log keeps prior findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** TypeScript changes (event; GitHub Actions or Claude Code routine; `push touching .ts or .tsx files`)
- **Verification:** types compile, switches exhaustive. Hard checks: tsc compiles after the type changes; the switch-exhaustiveness-check ESLint rule passes; repository conventions are respected over the guidance. On fail: retry, max 2 retries.
- **Memory:** union review log at `loops/discriminated-unions-review-loop/run-log.md`. Read first: prior findings and the repository's own conventions.

## Steps

1. **Read conventions.** Your agent inspects the repository's conventions and config, which take precedence over the guidance.
2. **Find candidates.** It finds types where optional properties or boolean flags hide mutually exclusive variants.
3. **Model variants.** It suggests a discriminated union with a shared literal discriminator per variant.
4. **Keep the line.** It leaves properties optional where they may independently be absent and does not force a union.
5. **Check exhaustiveness.** It confirms switches handle every variant via the ESLint rule.
6. **Build.** It compiles with tsc and records the findings.

Stop rule: Stops after one change set per run, with at most 2 fix retries.

## Permissions

- Writes: src/**, loops/discriminated-unions-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/discriminated-unions-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: TypeScript changes. Verification: types compile, switches exhaustive. Memory: loops/discriminated-unions-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
