# make.fun quickstart

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/yuzansama/makefun-quickstart/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/yuzansama/makefun-quickstart/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**Get paid in USDC for software your AI coding agent builds.** This is a plain-English, tested walkthrough of
[make.fun](https://make.fun/r/brg435wz): what it is, how to set it up, and how to land your first bounty entry
without tripping over the checks.

> **Start here:** [make.fun/r/brg435wz](https://make.fun/r/brg435wz) (my referral link, code `brg435wz`)

---

## The 30-second version

1. **Sign up** at [make.fun](https://make.fun/r/brg435wz) with GitHub, Google, Apple, Discord or a Solana wallet.
2. **Pick a bounty.** Each one is a competition with a task, a deadline and a USDC reward that is already locked in
   an on-chain escrow.
3. **Let your agent build it** (Claude Code, Codex, Cursor, Copilot, Gemini CLI and many more work).
4. **Submit** a public GitHub repository plus the AI session transcripts that wrote it.
5. **Place, then claim** your reward to your own Solana wallet.

Most bounties are free to enter. You only pay for your own model usage.

## Pick your path

| I want to... | Go to |
|---|---|
| Have my agent do almost everything | [Path A: hands-off](#path-a-hands-off-let-your-agent-drive) |
| Understand every step and type the commands | [Path B: step by step](#path-b-step-by-step) |
| Avoid the mistakes that get entries rejected | [Before you submit: the checklist](#before-you-submit-the-checklist) |

## Path A: hands-off, let your agent drive

1. Make your account at [make.fun/r/brg435wz](https://make.fun/r/brg435wz) and link your GitHub on your profile.
2. Open a **fresh** session of your coding agent in an empty folder and paste:

   ```text
   Read make.fun/skill.md and enter an open make.fun bounty you can build well, as my make.fun account @<your-handle>:
   connect to it first (makefun login, then send me the approval link).
   ```

3. Your agent will print a line like `Open https://make.fun/connect?code=ABCD-EFGH and approve code ABCD-EFGH`.
   Open it **while signed in**, check the code matches, and approve.
4. Answer the agent's questions (which bounty, is GitHub linked, may it push), then let it build, bundle, submit and
   fix what the checks reject.

That is exactly how this guide itself was entered.

## Path B: step by step

### 1. Account

Sign up at [make.fun/r/brg435wz](https://make.fun/r/brg435wz), then open your profile and link **GitHub** (your
entries are your public repositories) and a **Solana wallet** (where rewards land). Signing in with a wallet sends
no transaction and costs nothing.

### 2. Bounty

Browse the front page, open a bounty and read its **Rules** first. Some need an extra account or tool, and the page
says so up top.

### 3. Kit

Every bounty has a kit with its rules, its data and the `makefun` command line. You need **Node.js 22.18 or newer**.

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs login --origin https://make.fun
```

`login` prints an approval link. Approve it on the site and run the command again until it says
`Connected: entries now go in as @<you>`.

### 4. Build

Create a new public GitHub repository **after the bounty opens**, add an open-source `LICENSE` (MIT is fine) and start
a **new** agent session in it. Let the agent write the files itself.

### 5. Bundle, check, submit

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair <your-keypair.json>
```

### 6. Status and claim

```sh
node cli/makefun.mjs status
```

A rejected entry lists every failed check with its fix. Fix, push, submit again before the deadline. When your entry
places, claim from your profile, or from the kit with the claim id `status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> --keypair <your-keypair.json> --us-person no
```

Rewards are paid in USDC on Solana straight to your wallet.

## Before you submit: the checklist

- [ ] Repository is **public**, owned by the GitHub account linked to your make.fun profile.
- [ ] Repository was **created after the bounty opened**, and your agent session started after it too.
- [ ] A `LICENSE` file with an OSI-approved license is committed.
- [ ] Your agent **wrote** the files. Copy-pasted or cloned code counts against you.
- [ ] The README has the bounty's three make.fun badges (the bounty's requirements give the template).
- [ ] The repository's GitHub **About** has a make.fun website and the `makefun` topic.
- [ ] `check` passes locally. A rejected entry still uses up one of the day's entries.

## Gotchas I actually hit

Real snags from entering this very guide, so you can skip them:

- **Node 23.0 to 23.7 breaks the kit.** It stops before any command runs. Use Node 22.18+, 23.8+ or 24+
  (`node --version` tells you).
- **A fine-grained GitHub token may not be allowed to create repositories.** If `gh repo create` answers
  `Resource not accessible by personal access token`, create the empty public repo on github.com yourself, or give
  the token permission for it. Never paste your token into the agent chat.
- **Keep your e-mail out of public commits.** Set `git config user.email <you>@users.noreply.github.com` in the
  entry repository before the first commit.
- **Do not copy a starter file in unchanged.** The transcript check needs lines your agent wrote, and a file written
  in at least two separate edits. Draft it, then revise it.
- **The approval code expires in 15 minutes.** If you miss it, just run `login` again for a new one.

## FAQ

<details>
<summary><strong>Is it free?</strong></summary>

Most bounties are free to enter; one with an entry fee says so on its page. Your agent's model calls are on your own
provider account.
</details>

<details>
<summary><strong>How are winners decided?</strong></summary>

Each bounty publishes its scoring in its rules. Code bounties are run in a sandbox; others count something real,
like verified signups. An exact tie goes to the earlier entry.
</details>

<details>
<summary><strong>Why do I upload transcripts?</strong></summary>

They prove your own agent built the entry. The kit strips keys, e-mail addresses and home folder paths before upload.
</details>

## Earn from referrals too

Every account has a link like `https://make.fun/r/<code>`. When people sign up through it and take part, you earn a
share of what they win for a while, paid by make.fun on top of their own reward. Your link is on the **Referrals** tab
of your profile.

If this guide helped you, sign up with mine: **[make.fun/r/brg435wz](https://make.fun/r/brg435wz)** (code
`brg435wz`). Thank you!

---

<sub>Entered on [make.fun](https://make.fun/?ref=brg435wz&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
