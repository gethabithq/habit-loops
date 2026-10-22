---
name: ant-design
title: Ant Design skill
repo: ant-design/antd-skill
license: MIT
url: https://gethabit.dev/skills/ant-design/ant-design
---

# Ant Design skill

Ant design is a decision guide for antd 6.x, Ant Design Pro and Ant Design X, with an offline CLI for component API lookup, demos, theming tokens, SSR, linting and migration. For React developers building with Ant Design.

- Install the skill: `npx skills add ant-design/antd-skill --skill ant-design`
- Source: https://github.com/ant-design/antd-skill/tree/HEAD/skills/ant-design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You pick or wire an antd component; You theme with design tokens; You set up SSR or migrate antd.
Skip it when: You use a different UI library; You build a non-React app.

# Make it a habit: antd code uses real, current APIs.

On pull requests that touch Ant Design code, your agent looks up each component's API with antd info --format json before judging it, checks tokens-first theming and SSR, then runs antd lint on the changed paths. It never relies on memory or internal .ant- selectors.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** antd code changes (event; GitHub Actions or Claude Code routine; `pull_request paths: src/**`)
- **Verification:** info + lint. Hard checks: antd info --format json was queried for each changed component; antd lint --format json passes on the changed paths; no internal .ant- selector is used; no undocumented prop, event or component name is used. On fail: notify, max 1 retries.
- **Memory:** antd review log at `loops/antd-api-check-loop/log.md`. Read first: the antd version and open issues from earlier runs.

## Steps

1. **Classify the layer.** Identify core antd, Pro or X and confirm the version and rendering mode.
2. **Query the API.** Run antd info --format json for each changed component instead of relying on memory.
3. **Check theming.** Confirm tokens first, then classNames and styles, with one root ConfigProvider.
4. **Check SSR and a11y.** Verify the SSR style order, stable rowKey on tables and controlled Upload modes.
5. **Lint.** Run antd lint --format json on the changed paths and fix findings.
6. **Log.** Record the version and any issues for the next run.

Stop rule: Stops after the changed components of one pull request, with 1 retry.

## Permissions

- Writes: loops/antd-api-check-loop/**
- Network: ant.design
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/antd-api-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: antd code changes. Verification: info + lint. Memory: loops/antd-api-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
