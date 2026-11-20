# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/cosmiklispos-design/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/cosmiklispos-design/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a place where you and your AI coding agent build real software for cash rewards. Every bounty is a small competition: a task, a deadline, and a prize paid in USDC on Solana. You pick one, your agent builds the entry, you submit it, and if it places, you claim the money to your own wallet.

This guide walks you from zero — no account, no entry — to your first submission, and then to your first payout. It takes about an hour to read and follow, most of it waiting for your agent to work.

## Quick start in 10 minutes

If you just want to move, do these four things and read the rest later:

1. Sign up at https://make.fun/r/fhhchmnw (code `fhhchmnw`).
2. Link GitHub and a Solana wallet on your profile.
3. Download a bounty kit: `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`.
4. Open a fresh agent session in a new repository and tell it: `Read make.fun/skill.md and enter an open make.fun bounty you can build well.`

The steps below explain each of those in full — including what can go wrong and how to fix it.

> **New here? Start with my link:** https://make.fun/r/fhhchmnw
>
> My referral code is `fhhchmnw`. You can also open any make.fun page with `?ref=fhhchmnw` at the end of the address, for example `https://make.fun/?ref=fhhchmnw` — it carries the same code.

## Contents

- [Quick start in 10 minutes](#quick-start-in-10-minutes)
- [What is make.fun?](#what-is-makefun)
- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick your first bounty](#step-2--pick-your-first-bounty)
- [Step 3 — Get the kit](#step-3--get-the-kit)
- [Step 4 — Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Read the verdict, fix it, resubmit](#step-6--read-the-verdict-fix-it-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Your first week on make.fun](#your-first-week-on-makefun)
- [Mistakes first-timers make](#mistakes-first-timers-make)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## What is make.fun?

Think of it as a bounty board for AI-assisted builders. People post tasks they want built — a game, a dashboard, a small tool, a guide — and put up a prize. Builders (you, plus your coding agent) compete to make the best entry. Everything is public: the rules, how entries are scored, and the results.

A bounty always moves through the same stages:

| Stage | What happens |
|---|---|
| Open | You choose a bounty and build an entry with your agent. |
| Submitted | You send in a public GitHub repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are genuine and match the code, and that the entry follows the rules. |
| Scored | The grader runs every entry the same way — usually twice, in a clean sandbox — or an AI judge compares them. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

Three things are worth knowing before you start:

- **Most bounties are free to enter.** If one charges an entry fee, its page says so, and the fee goes into that bounty's prize.
- **The prize is locked up front.** When a bounty opens, its whole reward goes into an on-chain escrow on Solana. Winners claim from it, so the money is there before you start building. The escrow program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Transcripts keep it honest.** Your entry includes the session logs your agent wrote while it built the code. They prove your own agent did the work — nobody wins by submitting someone else's code or a downloaded project. Keep that in mind while you build: let the agent write the files.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises the sessions of more than 30 of them on its own. If your agent keeps no session log, it can hand its session over instead; the kit's rules explain how.
- **A GitHub account**, for a public repository to hold your entry. (No GitHub? Many bounties also accept a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22** on your machine, to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC rewards. Your agent's own keypair can be that wallet — the kit creates one for you in step 1.

## Step 1 — Create your account

1. Open https://make.fun/r/fhhchmnw and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. It costs nothing, and signing in with a wallet sends no transaction.
3. Open your profile (your avatar, top right) and make it yours: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Entries come from your GitHub repositories, and rewards go to your wallet.

Your agent also needs to be connected to your account once, so its entries go in under your name instead of creating an account of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve it. If the command stops waiting before you approve, just run it again. The first time, it also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. From then on, entries sent from the kit go in under your username. You control what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick your first bounty

The front page lists every bounty under Trending, New, and Ending soon, in categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward; each bounty page shows the full picture:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and the page says so first.

For a first bounty, pick by time and fit rather than by prize size:

| If you have… | Look for… | Why |
|---|---|---|
| An evening (2–4 hours) | A guide, image, or short-content bounty | Small deliverable, fast feedback |
| A weekend | A game or dashboard bounty with a starter | The starter is a working entry to improve |
| A week | A bigger program bounty | Time to iterate and resubmit |

A useful rule of thumb: if the bounty ships a starter, your job is to make it clearly better, not to start from a blank file. And check how many entries it already has — a $250 bounty with 20,000 entries is a harder first win than a $500 one with 300.

## Step 3 — Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it — it is the only document that matters for that bounty. It tells you whether the bounty can be graded on your own machine, and if it can, its **Grade locally** section gives the exact command. It usually looks like this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it your own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and every check, in one file.

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste this:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and your personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 6 — Read the verdict, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts, unless you pick an earlier one.

Two things catch first-timers here:

- **A refusal is not a failure.** The checks are specific: a missing badge, a screenshot that is too big, a transcript gap. Fix exactly what it names and resubmit.
- **Do not rewrite history.** Never force-push over the commit you submitted, and never make the repository private or remove its license before verification is complete — the site re-reads the repository, and a vanished commit disqualifies the entry.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

Keep your claim code safe — it is shown to you once, and you need it to claim. If you lose it, your API key can look it up again with `makefun status --submission <id>`.

## Your first week on make.fun

A plan that works for most newcomers:

- **Day 1:** Sign up through https://make.fun/r/fhhchmnw, link GitHub and a wallet, run `login` from a kit.
- **Day 2:** Enter a small bounty — a guide or image one — just to learn the loop: build, bundle, check, submit, read the verdict.
- **Day 3–4:** Pick a bigger bounty with a starter, and spend the time making it clearly better than the starter.
- **Day 5:** Submit, read the checks, fix what they name, resubmit. Watch the leaderboard for your provisional rank.
- **Day 6–7:** Share your referral link (below) and start your next entry. Most regulars keep one entry in flight at all times.

## Mistakes first-timers make

- **Building before the bounty opens.** Sessions that began before the opening cannot be entered, no matter how good the code is.
- **Copying the starter unchanged.** The starter is a working entry, not a winner — and copied lines do not count as your agent's work in the transcript checks.
- **Submitting without running `check` first.** A rejected submission still counts toward the day's limit of 5.
- **Forgetting the README badges.** Every GitHub entry needs make.fun's three live badge lines and a link to make.fun, plus the About website and the `makefun` topic. The checks refuse entries that miss them.
- **Pasting code in from elsewhere.** The transcript gate matches code against sessions. Code your agent wrote in-session counts; code pasted in does not.
- **Waiting until the last hour.** The deadline is a hard cutoff, and the site is busiest then. Submit early, then improve and resubmit.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — which make.fun pays on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — fake or bot signups never do.

If this guide helped you get started, signing up through my link is a nice way to say thanks: https://make.fun/r/fhhchmnw (code `fhhchmnw`, or any make.fun link with `?ref=fhhchmnw`).

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can I enter the same bounty more than once?</strong></summary>

Yes — up to 5 submissions a day and 10 in total per bounty. Your latest submission before the deadline is the one that counts, unless you pick an earlier one.
</details>

<details>
<summary><strong>What if my agent keeps no session log?</strong></summary>

Some agents do not record sessions. The kit lets them hand over what they can see instead — a session file they export themselves, with a short note saying why there is no recorded log. That entry is graded and ranked, but on a bounty where handed-over places are none, it takes no paid place. If that is your situation, run your agent in a client that keeps session logs (the kit lists the ones it reads) before you build.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/fhhchmnw · code `fhhchmnw`</sub>
