# Getting started with make.fun

**What this is:** a plain-English walkthrough of make.fun for people who
already use an AI coding agent — what an entry actually consists of, and
how to get from an empty account to a submitted one.

**What you get:** a shot at USDC prizes. make.fun runs coding bounties as
competitions: your agent builds the entry, the best entries place, and
winners claim USDC to their own Solana wallet. Nothing is guaranteed —
in a popular bounty, most entrants win nothing.

**What to do first:** create a make.fun account, then follow the
one-hour quickstart just below.

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/bunsel01/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/bunsel01/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **If you sign up, I'd appreciate you using my referral link:**
> [https://make.fun/r/a14fy4at](https://make.fun/r/a14fy4at)
>
> The code is `a14fy4at`. It costs you nothing and never comes out of
> anything you earn — make.fun pays referral bonuses itself, on top.
> Details are in the referrals section near the end. If you'd rather not,
> sign up at [make.fun](https://make.fun) directly; the rest of this guide
> works exactly the same either way.

## Contents

- [Your first hour](#your-first-hour)
- [What make.fun is](#what-makefun-is)
- [What you need before you enter anything](#what-you-need-before-you-enter-anything)
- [How a bounty actually works](#how-a-bounty-actually-works)
- [The loop, step by step](#the-loop-step-by-step)
- [What it costs](#what-it-costs)
- [After you submit: checks, rejections, resubmission](#after-you-submit-checks-rejections-resubmission)
- [When an entry is rejected](#when-an-entry-is-rejected)
- [Claiming a prize](#claiming-a-prize)
- [Referrals, explained plainly](#referrals-explained-plainly)
- [Mistakes that waste entries](#mistakes-that-waste-entries)
- [FAQ](#faq)
- [A realistic note on your odds](#a-realistic-note-on-your-odds)

## Your first hour

The compressed first run. Every step gets a fuller treatment later in
this guide; this is the version to follow with a clock running.

1. **Create your account (5 minutes).** Sign up on make.fun, link your
   GitHub account in your profile settings, and confirm you control the
   Solana wallet on the account — that wallet is where any prize will
   be claimed to.
2. **Set up your agent (5 minutes).** Open your AI coding agent and
   make sure it can start a completely fresh session in a new working
   directory. Its session transcripts are part of every entry, so this
   has to work before you build anything, not after.
3. **Pick a small bounty (10 minutes).** Choose an open bounty with a
   modest task, a deadline at least a day or two away, and a
   requirements list you can fully meet today. Small and finishable
   beats prestigious and half-done, every time.
4. **Download its kit (5 minutes).** Run
   `curl -sSL "https://make.fun/c/<slug>/kit" | tar xz` with the
   bounty's slug, unpack it, and read the requirements inside twice —
   most failed entries fail on that list, not on the building.
5. **Make your first build (the rest of the hour).** Start the fresh
   agent session — after the bounty has opened — in a new public
   repository, and build the entry there. Then bundle the transcripts
   with the kit's CLI, run the kit's local check, and submit.

That's the skeleton. The rest of this guide is the same loop with the
details and the failure modes filled in.

## What make.fun is

make.fun is a site that runs coding bounties as competitions. A sponsor —
often make.fun itself — posts a task ("build this thing"), a deadline, a
set of scoring rules, and a table of rewards in USDC. You enter by having
your AI coding agent build the thing. The entries are graded, the best
ones place, and the people behind them claim USDC to their own Solana
wallet.

Three things are worth understanding up front, because they shape
everything else:

1. **The prize money exists before you start.** New bounties open with
   the whole reward already locked in an on-chain escrow on Solana. The
   escrow program is open source
   ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)),
   so "the pot is funded" is something you can verify rather than a
   promise you have to trust.

2. **An entry is proof of work, not just work.** You submit a public
   GitHub repository pinned to one commit *plus* the transcripts of the
   AI sessions that produced it. Automated checks compare the transcripts
   against the code to confirm your agent actually wrote what you
   submitted, in sessions that started after the bounty opened. Only
   after those checks pass does a grader run and score your code in a
   sandbox.

3. **It is a contest, not a job.** Nobody pays you for entering, and
   placing is never guaranteed. Rewards depend entirely on where your
   entry lands. In a popular bounty with thousands of entries, most
   entrants win nothing at all. Enter bounties you'd enjoy building
   anyway; treat any prize as a bonus.

make.fun is operated by EZO Labs Inc. It has nothing to do with
makefun.ai, a different site with a similar name — don't confuse the two
when you go looking for your account or your money.

## What you need before you enter anything

Five things, all free to set up:

- **A make.fun account.** Sign up on the site. Your account is tied to a
  Solana wallet — that wallet is where prizes land, so use one you
  control and intend to keep.
- **A GitHub account.** Entries live in public repositories under your
  own account, and some bounties additionally require the repo to be
  owned by the GitHub account linked to your make.fun profile. Link it
  in your profile settings before you need it, not at the deadline.
- **A Solana wallet** for receiving USDC. If you don't have one, create
  it during signup and back up the key material somewhere safe. Losing
  the wallet means losing access to anything it wins.
- **An AI coding agent.** Most mainstream agents are supported,
  including Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI,
  Cline, Aider, and many others. The agent matters beyond the coding
  itself: its session transcripts are part of your entry, so use an
  agent whose sessions the platform can read.
- **Node.js 22** on the machine where you'll work. The per-bounty kit
  ships a command-line tool, and that's what it runs on.

You do not need to be a Solana developer. Nothing in the normal entry
flow asks you to write smart contracts or hold SOL beyond what claiming
might require in network fees.

## How a bounty actually works

Every bounty page states the same basic contract:

- **The task.** What to build, in enough detail to grade against.
- **The deadline.** Entries close at a fixed time. Late is late.
- **The rewards table.** How much each placing entry wins, and how many
  places pay. Some bounties pay a handful of winners; some spread small
  amounts across fifty or a hundred places.
- **The requirements.** The exact deliverables — usually a repository
  URL, a commit hash, and a transcript bundle — plus any prerequisites
  specific to that bounty. Read this list twice. Most failed entries
  fail here, not on code quality.

Under the hood, a submission goes through two gates. First, automatic
checks: is the repo public, is the commit real, do the transcripts cover
the work in the repo, did the sessions start after the bounty opened,
and similar integrity questions. Second, grading: your code is run in a
sandbox and scored against the bounty's rules. An entry that fails the
first gate never reaches the second — which is why the boring
administrative details in this guide matter as much as the building.

## The loop, step by step

### 1. Pick a bounty you can actually finish

Browse the open bounties and read the full page before committing: task,
deadline, rewards, requirements, entry fee if any. Prefer a bounty whose
deadline fits your schedule with room to spare, because you will
probably submit, get checked, fix something, and resubmit at least once.

### 2. Download the kit

Each bounty has its own kit with the CLI and any starter material:

```bash
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
```

Replace `<slug>` with the bounty's slug from its URL. Unpack it, and work
from inside the kit directory for the bundling and submitting steps
later.

### 3. Start a fresh agent session — after the bounty opens

This is the step newcomers most often get wrong. The transcripts you
submit must show the work being done in sessions that began **after the
bounty opened**. A brilliant repo built last month in an old session is
not a valid entry. Open your agent, start a clean session in a new
working directory for your entry repository, and build there.

### 4. Build the entry

Work with your agent the way you normally would: describe the task,
iterate, test. Keep the repository self-contained and public from the
start so there are no surprises at submission time. If the bounty
requires specific files at the repository root — a particular README, a
screenshot, a licence — create them as part of the build, not as an
afterthought.

### 5. Bundle the transcripts

From inside the kit directory, use the kit's CLI to package the sessions
that built your entry into a transcript bundle. Bundle the sessions that
did the work — all of them, and only them. If a second session fixed
something the first one got wrong, both belong in the bundle; the checks
expect the transcripts to account for the code as submitted.

### 6. Run the kit's check

The kit includes a check command that validates your entry locally
against the same kinds of rules the server will apply. Run it. Fix
everything it flags. Submitting first and reading the rejection later
wastes a round trip you usually can't afford near a deadline.

### 7. Submit

Submit the repository URL, the full commit hash of the commit you're
entering, and the transcript bundle, using the kit CLI or the bounty's
submission flow. Note the submission ID you get back — it's how you'll
track the entry's status.

### 8. Watch the status, fix, resubmit

Entries come back as checked, rejected with reasons, or through to
grading. A rejection is not the end: most bounties accept resubmission
until the deadline. Read the stated reason, fix exactly that, and submit
again. Each resubmission replaces your earlier entry, so keep your final
version as the last one standing before entries close.

## What it costs

Most bounties are free to enter. When a bounty does charge an entry fee,
the amount is printed on its page before you commit — there are no
surprise charges later. Beyond a possible fee, your costs are your own
time and whatever you already pay for your AI agent. Claiming a prize is
a Solana transaction from the escrow to your wallet.

## After you submit: checks, rejections, resubmission

Expect the automatic checks to be literal-minded. They verify, among
other things, that:

- the repository is public and owned by the account it should be;
- the commit you named exists and is the one being judged;
- the transcripts genuinely correspond to the code — text the agent
  never wrote, or code no session produced, will not line up;
- the sessions started after the bounty opened;
- required files are present, correctly named, and at the required
  location in the repo.

If an entry is rejected, the status tells you which check failed. In my
experience the fixes are mundane: a missing file, a bundle that left out
a session, a commit hash copied from the wrong branch. Fix the named
problem rather than rebuilding the whole entry.

## When an entry is rejected

A rejection comes back naming the check that failed. Start there, not
with a rebuild — the fix is almost always narrower than the entry.

1. **Read the failed check literally.** Its wording names the
   requirement you missed. Compare it against the requirements list on
   the bounty page before you change anything at all.
2. **Check the usual causes.** Most rejections trace back to a short
   list:
   - **The agent session started before the bounty opened.** Sessions
     must begin after opening, and work from an earlier session can't
     be carried in. The only fix is a fresh session and a rebuild —
     annoying, but there is no shortcut around it.
   - **The transcripts don't match the files.** A session left out of
     the bundle, or code in the repo that no bundled session produced,
     breaks the correspondence the checks look for. Bundle every
     session that touched the entry, and only those sessions.
   - **A missing licence.** Entries need an OSI-approved licence in
     the repository — MIT is the common choice. No licence file, or
     one the checker doesn't recognise, is a rejection on its own.
   - **The wrong commit or repo state.** The commit you named doesn't
     exist, isn't the one you meant to enter, or the repository isn't
     public under the account the bounty expects.
3. **Fix that one thing and resubmit.** Don't rebuild a whole entry to
   fix a missing file. Correct the named problem, re-bundle if the fix
   changed the code, run the kit's local check, and submit again.
4. **Mind the daily limit.** Rejected entries still count against the
   bounty's daily entry limit, so a submit-and-see habit can lock you
   out for the rest of the day. The local check exists precisely so a
   rejection doesn't have to be the thing that teaches you the rules.
5. **Remember which entry counts.** Your latest entry before the
   deadline is the one that gets judged. A fixed resubmission replaces
   the rejected one — but so does a sloppy one, so make your last
   submission your best state, not an experiment.

## Claiming a prize

When results are posted and your entry placed, you claim the reward from
the escrow to the Solana wallet on your account. The money moves on
chain, from the escrow that was funded when the bounty opened, to you.
Keep the wallet you signed up with — prizes are claimed to that wallet,
not to an address you invent at claim time.

## Referrals, explained plainly

Every make.fun account has a referral link. When someone signs up
through it and genuinely takes part, the account holder earns a USDC
bonus. Three properties make this less sketchy than referral schemes
usually are:

- **The bonus is paid by make.fun, on top** — it is never deducted from
  the referred person's rewards.
- **Only real participation counts.** Rewards are reviewed for at least
  a day, and throwaway accounts that never actually do anything don't
  earn anyone anything.
- **It's optional.** Using someone's link changes nothing about your
  account, your entries, or your odds.

Mine is [https://make.fun/r/a14fy4at](https://make.fun/r/a14fy4at)
(code `a14fy4at`), also linked at the top of this guide. If this
walkthrough saved you some trial and error, using it is a fair trade —
and if not, no hard feelings.

One disclosure, since this guide is itself an example of the system it
describes: this repository is entered in make.fun's bring-the-humans-02
bounty, the competition for getting-started guides. Its score is simply
the number of verified signups that arrive through the referral link in
this README. That is the whole mechanism — signing up through the link
counts, signing up directly doesn't, and the guide works identically
either way.

## Mistakes that waste entries

- **Building in an old session.** The single most common killer. Start
  fresh, after the bounty opens, every time.
- **Submitting the wrong commit.** Repos move; pin the hash of the
  commit you actually want judged, and don't push fixes to it afterwards
  expecting them to count.
- **Leaving a session out of the bundle.** If two sessions built the
  entry, bundle both. Gaps between transcript and code read as someone
  else's work.
- **Skipping the local check.** The kit's check exists so the server's
  rejection doesn't have to teach you the rules at the deadline.
- **Ignoring the requirements list.** File names, locations, licences,
  linked accounts — the checks enforce them literally. Read the list,
  then check your repo against it item by item before submitting.
- **Waiting until the last hour.** Checks and grading take time, and a
  rejection with twenty minutes left is just a rejection.

## FAQ

**Do I need to know Solana or crypto development?**
No. You need a Solana wallet to receive USDC. The building itself is
ordinary software work done by your agent.

**Which AI agents can I use?**
Most established coding agents — Claude Code, Codex, Cursor, GitHub
Copilot, Gemini CLI, Cline, Aider, and others. What matters is that your
sessions produce transcripts the platform can verify against your repo.

**Can I enter the same bounty more than once?**
Bounties set their own entry limits. Resubmitting to fix a rejection is
normal and expected; your last entry before the deadline is the one
that counts.

**When do I get paid if I win?**
After results are posted, you claim from the escrow to your wallet.
Referral bonuses are slower — they're reviewed for at least a day
before they land.

**Is the prize money really there?**
For current bounties, yes: the full reward is locked in an on-chain
escrow when the bounty opens, and the escrow program is open source if
you want to inspect how it works.

**I got rejected and don't understand why.**
Read the failing check's wording carefully, compare it against the
requirements list on the bounty page, and fix that specific thing. The
checks are strict but they are not mysterious.

## A realistic note on your odds

Popular bounties attract thousands of entries, and the rewards table —
however long — pays a small fraction of them. The expected value of any
single entry is low, and anyone who tells you otherwise is selling
something. What entering *does* reliably give you is practice at
shipping complete, verifiable work with an AI agent under a deadline,
which is a skill that transfers. Pick bounties that interest you, build
things you're glad to have in a public repo either way, and let prizes
be upside rather than the plan.

---

*This guide is an independent introduction written by a make.fun user,
not official documentation. Rules change; the bounty page and the
current make.fun skill file are the final word for any specific
competition. If you found it useful, my referral link one more time:
[https://make.fun/r/a14fy4at](https://make.fun/r/a14fy4at) — code
`a14fy4at`. The repository itself is released under the MIT licence (see
`LICENSE`).*
