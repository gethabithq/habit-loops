---
name: solana-dev
title: Solana Dev skill
repo: solana-foundation/solana-dev-skill
license: MIT
url: https://gethabit.dev/skills/solana-foundation/solana-dev
---

# Solana Dev skill

The solana dev skill is an end-to-end playbook for Solana: wallet connection, Anchor and Pinocchio programs, Kit clients, Surfpool and LiteSVM testing, security review and v1 transactions. For developers building Solana dapps and programs.

- Install the skill: `npx skills add solana-foundation/solana-dev-skill --skill solana-dev`
- Source: https://github.com/solana-foundation/solana-dev-skill/tree/HEAD/skills/solana-dev
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write an Anchor program; You connect a wallet in React; You debug Solana errors.
Skip it when: You build on another chain; You only need one balance lookup.

# Make it a habit: Solana changes built, tested, risk-noted.

When a pull request changes a Solana program or client, your agent classifies the layer, builds and tests with Anchor and Surfpool on localnet, checks v1 transaction rules and writes risk notes. Any signing waits for your approval. A board keeps open risks.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes Solana code (event; GitHub Actions or Claude Code routine; `pull_request paths: programs/**, Anchor.toml, client code using @solana/kit`)
- **Verification:** tests pass, you sign. Hard checks: NO_DNA=1 anchor build succeeds; NO_DNA=1 anchor test passes; no ComputeBudget instructions on v1 transactions; simulateTransaction runs before any signature request. On fail: notify, max 1 retries.
- **Memory:** open risk notes at `loops/solana-program-check-loop/board.md`. Read first: risk notes on signing, fees, CPIs and token transfers still open.

## Steps

1. **Classify the layer.** Sort the change into UI, client, program, testing or infra, using the Solana MCP server for current docs.
2. **Check correctness.** Confirm cluster, fee payer, transaction version, account owners, signers and token program variant.
3. **Build and test.** Run NO_DNA=1 anchor build and NO_DNA=1 anchor test with LiteSVM, Mollusk or Surfpool.
4. **Simulate first.** Run simulateTransaction on devnet or localnet and show the result.
5. **Ask before signing.** Show recipient, amount, token, fee payer and cluster, and wait for your approval.
6. **Write risk notes.** List changed files and a short risk section for signing, fees, CPIs or token transfers.

Stop rule: One pull request per run, one retry after a failed build, never mainnet without your explicit request.

## Permissions

- Writes: loops/solana-program-check-loop/**
- Network: mcp.solana.com, devnet and localnet RPC
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/solana-program-check-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes Solana code. Verification: tests pass, you sign. Memory: loops/solana-program-check-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
