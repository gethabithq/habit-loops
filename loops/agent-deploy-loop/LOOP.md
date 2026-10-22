---
name: google-agents-cli-deploy
title: Google Agents CLI Deploy skill
repo: google/agents-cli
license: Apache-2.0
url: https://gethabit.dev/skills/google/google-agents-cli-deploy
---

# Google Agents CLI Deploy skill

The google agents cli deploy skill by Google guides deploying agents with agents-cli to Agent Runtime, Cloud Run or GKE: CI/CD, secrets, service accounts, sizing, rollback and troubleshooting.

- Install the skill: `npx skills add google/agents-cli --skill google-agents-cli-deploy`
- Source: https://github.com/google/agents-cli/tree/HEAD/skills/google-agents-cli-deploy
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You deploy an ADK agent; You set up CI/CD for an agent; A deploy fails with 403.
Skip it when: You still write agent code; You only need evaluation.

# Make it a habit: Agents deployed only after your approval.

When eval scores are in, your agent pastes them with the test results and asks if you are ready to deploy to dev. On your yes it runs agents-cli deploy, polls the status, and tests the live agent with agents-cli run --url. A log keeps each deploy.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** eval scores ready (event; Claude Code routine; `agents-cli eval run finished with scores you agreed on`)
- **Verification:** your yes + live test. Hard checks: agents-cli deploy --status reports completion; agents-cli run --url answers a test prompt; deployment_metadata.json exists after an Agent Runtime deploy. On fail: notify, max 1 retries.
- **Memory:** deploy log at `loops/agent-deploy-loop/deploys.md`. Read first: the last deploy: target, flags, service URL and result.

## Steps

1. **Load related skills.** Your agent follows google-agents-cli-workflow, and uses google-agents-cli-scaffold if the project has no deployment target.
2. **Pick the target.** It asks you to choose Agent Runtime, Cloud Run or GKE, using the decision matrix.
3. **Enhance a prototype.** If there is no target yet, it runs agents-cli scaffold enhance . --deployment-target.
4. **Ask for approval.** It pastes the eval scores and test results and asks if you are ready to deploy to dev.
5. **Deploy.** Only after your explicit yes, it runs agents-cli deploy with the needed flags.
6. **Poll the status.** If the command times out, it runs agents-cli deploy --status every 60 seconds until done.
7. **Test live.** It runs agents-cli run --url with a prompt to test the deployed agent.
8. **Log.** It writes the target, URL and result to the deploy log, and notes google-agents-cli-publish for registration.

Stop rule: Stops after one deploy per run, or when the same error shows 3 times in a row.

## Permissions

- Writes: deployment/terraform/**, deployment_metadata.json, loops/agent-deploy-loop/**
- Network: Google Cloud (agents-cli and gcloud)
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/agent-deploy-loop/deploys.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: eval scores ready. Verification: your yes + live test. Memory: loops/agent-deploy-loop/deploys.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
