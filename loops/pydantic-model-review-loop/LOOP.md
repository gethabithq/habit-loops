---
name: pydantic
title: Pydantic skill
repo: pydantic/skills
license: MIT
url: https://gethabit.dev/skills/pydantic/pydantic
---

# Pydantic skill

The pydantic skill helps Python developers model data with Pydantic: field constraints, validators, coercion, forward annotations and safe model hierarchies with discriminated unions.

- Install the skill: `npx skills add pydantic/skills --skill pydantic`
- Source: https://github.com/pydantic/skills/tree/HEAD/plugins/pydantic/skills/pydantic
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add constraints to a model; You build a model hierarchy; You validate untrusted API input.
Skip it when: You only need internal dataclasses; You do not use Python.

# Make it a habit: Pydantic models use built-in validation.

On every pull request that touches Pydantic models, your agent checks for custom validators that a built-in constraint could replace, before validators where after would do, subclass fields lost on dump and stringified annotations. A log keeps findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** model files changed (event; GitHub Actions or Claude Code routine; `pull_request touches files importing pydantic`)
- **Verification:** tests pass, patterns hold. Hard checks: tests pass; no field_validator that only checks a simple bound like gt or max_length; no from __future__ import annotations in model modules; subclass fields use a discriminated union or generics. On fail: notify, max 0 retries.
- **Memory:** model review log at `loops/pydantic-model-review-loop/run-log.md`. Read first: earlier findings per module.

## Steps

1. **List models.** Collect changed BaseModel classes and their fields.
2. **Check constraints.** Prefer Field, annotated_types or StringConstraints over custom validators.
3. **Check validators.** Prefer after validators and the annotated AfterValidator form.
4. **Check hierarchies.** Replace base-typed subclass fields with a discriminated union or generics.
5. **Check annotations.** Flag string annotations and quoted recursive TypeAlias.
6. **Run tests.** Run the tests and log findings.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/pydantic-model-review-loop/**
- Network: pydantic.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pydantic-model-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: model files changed. Verification: tests pass, patterns hold. Memory: loops/pydantic-model-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
