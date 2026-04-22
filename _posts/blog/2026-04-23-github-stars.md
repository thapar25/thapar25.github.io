---
layout: post
title: Everyone in SF Knows GitHub Stars Are Fake. Nobody Cares.
date: 2026-04-23
tags:
  - AI
  - GitHub
  - open-source
  - oss
  - cybersecurity
description: The perception of GitHub stars as a reliable indicator of project quality has significantly diminished due to large-scale manipulation and their use as a "vanity metric".
---
## Are Star Histories OSS Milestones?

## Star History

![Star History Chart](https://api.star-history.com/chart?repos=raga-ai-hub/RagaAI-Catalyst%2Cnousresearch/hermes-agent&type=date&legend=top-left)

There's a repo on GitHub right now with 14,000 stars, a gorgeous README, and code that hasn't had a meaningful commit in eight months. You've probably starred something like it. So have I.

We all know what a GitHub star actually means in 2026: someone thought a project looked cool for thirty seconds. Maybe they were procrastinating. Maybe it showed up on Hacker News. Maybe someone in a San Francisco office spent $200 to make it look like traction before a seed round. Nobody says that last part out loud.

## The game everyone's playing

Here's how the SF open-source playbook works right now, and it's barely a secret.

You build a tool. You write a beautiful README with a snappy GIF. You post it to every subreddit, every Discord, every corner of the internet simultaneously. You call it a "day one launch." Then an AI influencer with 200k followers on X quote-tweets it with "this is going to be HUGE 🚀" without having run a single line of it. Three more influencers repost that. Stars pour in. If you're playing the game seriously, you might top it off with a few hundred purchased ones, because VC firms have [literal scrapers watching star velocity](https://www.redpoint.com/content-hub/written/so-how-many-stars-is-enough/), and [Runa Capital publishes a quarterly ranking](https://runacap.com/ross-index/) of open-source startups sorted almost entirely by 90-day star growth. Sixty-eight percent of those ranked companies subsequently raised funding.

You can buy 1,000 stars for around $64. [Providers are easy to find](https://awesomeagents.ai/news/github-fake-stars-investigation/): prices run from $0.10 to $2.00 per star, delivery in hours, no login required. Against a $2M seed round, that math writes itself.

The part that makes it funny, in a bleak way: [a peer-reviewed paper presented at ICSE 2026](https://arxiv.org/abs/2412.13459) by researchers at CMU, NC State, and Socket scanned 20 terabytes of GitHub data and found roughly **six million suspected fake stars** across 18,617 repositories. AI and LLM repos are now the single largest non-malicious category of recipients. GitHub's response has mostly been to quietly delete the flagged repos after someone else does the detective work.

## The actual product is the README

Stars don't just get bought. They get _gamed_ organically too, in a way that's arguably worse.

[OpenClaw](https://blog.bytebytego.com/p/top-ai-github-repositories-in-2026) went from 9,000 to 60,000 stars in a few days in January 2026, then blew past 210,000. Legitimately impressive. But it also set the benchmark everyone else is now trying to fake. The week it peaked, a dozen "autonomous agent frameworks" launched with nearly identical READMEs, riding the same wave of AI influencer reposts. Most were a `for` loop and some string formatting. A few bought stars to close the gap.

Here's the part the paper confirms that most people don't know: it doesn't even work. The CMU study found that fake stars produce a small bump in organic attention for at most two months, then become a net negative. Real users can smell something off. The lockstep patterns, hundreds of accounts starring the same repo in the same 30-day window with no other activity, register as a trust penalty once the algorithm catches up.

Stars measure whether something looked impressive during a 3-minute scroll. They have [almost no correlation](https://www.ndss-symposium.org/wp-content/uploads/madweb2024-4-paper.pdf) with whether the code works, whether it's maintained, or whether anyone actually runs it in production.

The engineers who've been building quietly for ten years know this. The maintainer of [SocketCluster](https://github.com/SocketCluster/socketcluster) put it plainly after watching his 6,000 legitimately-earned stars become meaningless:

> "It sucks having put in the effort and seeing it get lost in a sea of scams and seeing people doubting my project's own authenticity."

## Nobody's stopping

The honest answer is that the game continues because everyone's playing it and nobody wants to be the one who stops first.

VCs keep using stars as a lazy proxy for developer love because it's a number that fits in a spreadsheet. Founders keep optimising for stars because that's what gets VC meetings. AI influencers keep boosting every shiny new repo because engagement is engagement and nobody checks back in six months when the repo is abandoned. Developers keep using stars as a trust signal when picking dependencies because who has time to read the actual source.

And the end of that chain is darker than most people realise. The CMU paper found one repo with 111 stars, 109 of them fake, presenting as a Solana trading bot. Hidden inside: a `spawn()` call quietly executing a remote obfuscated script that drained wallets. That's where [the Stargazers Ghost Network](https://research.checkpoint.com/2024/stargazers-ghost-network/) went, 3,000 coordinated bot accounts selling fake stars as a distribution channel for malware, because a starred repo looks trustworthy enough to clone.

The people proposing fixes, like [fork-to-star ratios](https://gerus-lab.hashnode.dev/your-open-source-repo-has-10k-github-stars-half-of-them-are-fake), contributor counts, [download telemetry](https://about.scarf.sh/), and [OpenSSF scorecards](https://scorecard.dev/), are correct and will largely be ignored. The fix requires effort. The game only requires a credit card.

The GitHub star is not dead. It just means something different now. It means someone wanted you to think a project was popular. Whether it actually is, that part's still on you to figure out.