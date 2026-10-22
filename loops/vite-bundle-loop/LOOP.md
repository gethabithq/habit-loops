---
name: react-vite-best-practices
title: React Vite Best Practices skill
repo: asyrafhussin/agent-skills
license: MIT
url: https://gethabit.dev/skills/asyrafhussin/react-vite-best-practices
---

# React Vite Best Practices skill

The react vite best practices skill gives React developers 23 rules for Vite builds, code splitting, HMR, assets, environment variables and bundle analysis, ranked by impact.

- Install the skill: `npx skills add asyrafhussin/agent-skills --skill react-vite-best-practices`
- Source: https://github.com/asyrafhussin/agent-skills/tree/HEAD/skills/react-vite-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You configure Vite for React; Your bundle is too large; You add lazy-loaded routes.
Skip it when: Your app does not use Vite; You build a server-only app.

# Make it a habit: Your Vite bundle stays lean.

On every pull request your agent builds the React app, checks chunk sizes against the limit, reads the bundle report and reviews splitting and env vars against the skill's 23 rules. Bundle sizes go into a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR opened or updated (event; GitHub Actions or Claude Code routine; `pull_request.opened, pull_request.synchronize`)
- **Verification:** build passes, chunks small. Hard checks: the build passes; no chunk exceeds the chunkSizeWarningLimit of 500; client env vars use the VITE_ prefix and hold no secrets. Critic: claude-opus-5-5, pass at 17/20. On fail: notify, max 0 retries.
- **Memory:** bundle size log at `loops/vite-bundle-loop/runs.md`. Read first: chunk sizes from the last build.

## Steps

1. **Read the log.** The agent loads chunk sizes from the last build.
2. **Build the app.** The production build must pass.
3. **Check chunk sizes.** No chunk may cross chunkSizeWarningLimit, and growth since last run gets flagged.
4. **Analyze the bundle.** rollup-plugin-visualizer shows which dependencies grew.
5. **Check splitting.** Heavy routes load through React.lazy inside Suspense boundaries.
6. **Check env vars.** Only VITE_ variables reach client code, and none hold secrets.
7. **Log sizes.** Chunk sizes and the critic's notes go into the run log.

Stop rule: Stops after one build and one review per pull request.

## Permissions

- Writes: loops/vite-bundle-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/vite-bundle-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR opened or updated. Verification: build passes, chunks small. Memory: loops/vite-bundle-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
