---
name: graphql-operations
title: GraphQL Operations Guide skill
repo: apollographql/skills
license: MIT
url: https://gethabit.dev/skills/apollographql/graphql-operations
---

# GraphQL Operations Guide skill

GraphQL Operations Guide (the graphql-operations skill) guides writing queries, mutations and fragments against the project schema: named operations, variables, lean field selection, fragments and type generation. For client developers writing GraphQL.

- Install the skill: `npx skills add apollographql/skills --skill graphql-operations`
- Source: https://github.com/apollographql/skills/tree/HEAD/skills/graphql-operations
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: writing GraphQL queries or mutations; organizing operations with fragments; setting up type generation or linting.
Skip it when: you work on the server schema only; the project has no GraphQL.

# Make it a habit: Operations match the schema and lint.

When GraphQL operations change, your agent checks them against the project schema: named operations, variables not hardcoded values, only needed fields, id on cacheable types, then runs codegen and the linter. A run log keeps prior findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** operations change (event; GitHub Actions or Claude Code routine; `push touching .graphql documents`)
- **Verification:** schema, codegen, lint. Hard checks: every field, argument and enum used exists in the project schema; type generation runs without error; the GraphQL linter passes; no operation is anonymous. On fail: retry, max 2 retries.
- **Memory:** operations review log at `loops/graphql-operations-review-loop/run-log.md`. Read first: prior findings and the schema location.

## Steps

1. **Find the schema.** Your agent finds the schema from codegen.ts, graphql.config or apollo.config, or the SDL files.
2. **Check fields.** It confirms every field, argument and enum value used is defined by the schema.
3. **Check naming.** It confirms each operation is named and uses variables instead of hardcoded values.
4. **Check selection.** It flags over-fetching and confirms id is requested on cacheable types.
5. **Run codegen.** It runs type generation to confirm the operations are type-safe.
6. **Lint.** It runs the GraphQL linter and records any findings in the run log.

Stop rule: Stops after one change set per run, with at most 2 fix retries.

## Permissions

- Writes: GraphQL operation documents, loops/graphql-operations-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/graphql-operations-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: operations change. Verification: schema, codegen, lint. Memory: loops/graphql-operations-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
