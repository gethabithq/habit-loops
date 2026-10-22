---
name: gsap-react
title: GSAP React skill
repo: greensock/gsap-skills
license: MIT
url: https://gethabit.dev/skills/greensock/gsap-react
---

# GSAP React skill

The gsap react skill is the official GreenSock guide to GSAP in React and Next.js: the useGSAP hook, refs and scope, gsap.context() with cleanup, contextSafe callbacks and server rendering. For React developers adding animation.

- Install the skill: `npx skills add greensock/gsap-skills --skill gsap-react`
- Source: https://github.com/greensock/gsap-skills/tree/HEAD/skills/gsap-react
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You animate React or Next.js components; Animations keep running after unmount; You move from useEffect to useGSAP.
Skip it when: You use another animation library; Your app is not built on React.

# Make it a habit: No leaking GSAP animations in React.

When a pull request changes React components that use GSAP, your agent checks for useGSAP with a scope, ctx.revert() in useEffect cleanups, contextSafe for event handlers and no GSAP calls during server render. It keeps a list of fixed components.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes GSAP components (event; GitHub Actions or Claude Code routine; `pull_request touching React files that import gsap or @gsap/react`)
- **Verification:** cleanup and scope check. Hard checks: build passes; every useGSAP() call passes a scope; every gsap.context() inside useEffect returns a cleanup that calls ctx.revert(); no gsap or ScrollTrigger call runs at module top level during server render; useGSAP is registered with gsap.registerPlugin() before use. On fail: notify, max 0 retries.
- **Memory:** component findings list at `loops/gsap-react-cleanup-loop/findings.md`. Read first: components already fixed and ones still open.

## Steps

1. **Find components.** List React components in the diff that create GSAP tweens, timelines or ScrollTriggers.
2. **Check the hook.** Prefer useGSAP() from @gsap/react over useEffect, with a ref passed as scope.
3. **Check cleanup.** Where useEffect is used, make sure gsap.context() is reverted in the cleanup.
4. **Check handlers.** Wrap animations made in event handlers with contextSafe and remove the listeners on cleanup.
5. **Check SSR.** Make sure no GSAP code runs on the server in Next.js or similar.
6. **Report.** Post findings on the pull request and update the list.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/gsap-react-cleanup-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gsap-react-cleanup-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes GSAP components. Verification: cleanup and scope check. Memory: loops/gsap-react-cleanup-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
