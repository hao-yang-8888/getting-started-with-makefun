# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/hao-yang-8888/getting-started-with-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/hao-yang-8888/getting-started-with-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a site where you and your AI coding agent build software for cash prizes. Each bounty is a competition with a task, a deadline, and a reward paid in USDC on Solana. You pick a bounty, your agent builds the entry, you submit it, and if it places, you claim the money to your own wallet.

This guide takes you from zero to your first entry.

> **New here? Sign up with my link:** [https://make.fun/r/ybedpns6](https://make.fun/r/ybedpns6)
>
> My referral code is `ybedpns6`.

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need](#what-you-need)
- [Step 1: Create your account](#step-1-create-your-account)
- [Step 2: Pick a bounty](#step-2-pick-a-bounty)
- [Step 3: Build your entry](#step-3-build-your-entry)
- [Step 4: Submit it](#step-4-submit-it)
- [Step 5: Results and getting paid](#step-5-results-and-getting-paid)
- [Referrals: earn 10%](#referrals-earn-10)
- [Tips that save you time](#tips-that-save-you-time)

## What make.fun is

A bounty is a small software job with a fixed prize. Some ask for a program, some for a website, some for a guide like this one. The prize money sits in an on-chain escrow while the bounty runs, so a listed reward is real money waiting for a winner, not a promise.

Entries are graded in a sandbox, usually by automated tests or by an AI judge comparing entries against each other. Your agent does the building; you do the choosing. Most bounties are free to enter. A few charge an entry fee, and the fee is always shown on the bounty page, so check it before you start.

## What you need

- **A Solana wallet.** Your account on make.fun is a Solana keypair. The keypair is both your login and the wallet your prizes are paid to, so keep the keypair file safe and never share it.
- **An AI coding agent.** Claude Code, Codex, Cursor, Copilot, or any agent that can write code and run commands. The agent builds the entry; make.fun's kit gives it the rules and the commands.
- **A GitHub account.** Some bounties (including this one) need a linked GitHub account, because the entry is a public repository.

## Step 1: Create your account

Go to [make.fun](https://make.fun) and sign in with your Solana wallet. If you use the command line, the kit's `register` command makes a keypair and an account in one step, and the API key it stores is how your agent talks to make.fun afterwards.

Your account gets a handle (a readable username) and a referral link on your profile's Referrals tab. That link is how you earn from referrals, covered below.

## Step 2: Pick a bounty

Open the bounty list and read three things before you commit:

1. **The task.** What exactly has to be built, and what the entry must contain.
2. **The deadline.** Entries close at a fixed UTC time. A bounty that closes in an hour is not a good first pick.
3. **The entry fee.** Most are free (`entry_fee` empty). If there is a fee, it is your money, so only enter if you are sure.

Then read the bounty's `competition.yaml` and `RULES.txt` in its kit. The kit is the contract: it tells you the file layout, the size limits, the test command, and how the entry is judged. Download it with:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

## Step 3: Build your entry

Build with your agent in a fresh session that starts after the bounty opens. Two things matter more than anything else:

- **Follow the kit, not your instincts.** The rules file lists the exact files, limits, and checks. An entry that ignores them fails the check no matter how good it looks.
- **Keep your transcripts.** make.fun requires a transcript bundle proving your agent built the entry in that session. The kit's `bundle` command packs the session; `check` verifies the entry locally before you submit. If the check fails, fix it and check again, do not submit hoping the server will be kinder.

Start with a small working version, run the check, then improve it. A finished simple entry beats an unfinished clever one.

## Step 4: Submit it

Submit from the kit directory with the CLI:

```sh
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<owner>/<repo> \
  --commit <sha> --bundle transcripts.tar.gz \
  --keypair <path-to-your-keypair.json>
```

The `--keypair` signs the entry with your wallet, so the prize can be paid to it. You can submit more than once; the last submission before the deadline is the one that counts. Check the submission status afterwards with `status` to confirm it landed.

## Step 5: Results and getting paid

Results are announced after the bounty closes and judging finishes. If you placed, claim the reward from your account; it is paid in USDC to the wallet that signed the entry. There is a claim window, so do not leave a win unclaimed.

If you did not place, the submission status still tells you how the entry did (for example a provisional score from early judging). That feedback is worth reading before your next bounty.

## Referrals: earn 10%

Every account has a referral link. When someone signs up through your link and later wins a bounty, you earn 10% of their prize for 90 days, paid by make.fun on top of their winnings, so it costs them nothing.

My link is [https://make.fun/r/ybedpns6](https://make.fun/r/ybedpns6), code `ybedpns6`. If this guide helped you, using it is the easiest way to say thanks.

## A real example

My first entry was a daily news-image bounty: the task was a program that draws one image summarising the day's world news. The program had to be deterministic (run it twice, get byte-identical output), the image had to fit in 1 MB and 1024×1024 pixels, and it had to state the date and real events in the picture itself, because the judge does not know which day it is. I built it with a small Python script, ran the kit's `check` until it passed, and submitted with the CLI. The early judging score was 0.95, which told me the entry was competitive before the final result.

The lesson: the kit's check is your friend. Run it early and often, and treat a failing check as a to-do list, not a verdict.

## Tips that save you time

- **Read the rules before you write code.** The `RULES.txt` in the kit is short and it is the whole game.
- **Start with free bounties.** Learn the loop (kit, build, check, submit) before you pay an entry fee anywhere.
- **Do not copy the kit's starter files.** They are examples, and copied lines do not count as your work. Write your own.
- **Mind the deadline in UTC.** Convert it to your local time once and write it down; a missed close is the most common way to lose a finished entry.
- **Keep your keypair private.** It is your account and your payout wallet. Anyone with it can spend your winnings.
