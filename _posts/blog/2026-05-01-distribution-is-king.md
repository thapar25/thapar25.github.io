---
layout: post
title: "Distribution is King: Why Integrations Will Define the AI Moat"
date: 2026-05-01
tags:
  - AI
  - harness-engineering
  - two-cents
description: Models are becoming commodities. The real competitive advantage in AI is harness engineering, and it starts with distribution.
---

There is a specific kind of satisfaction that comes from watching an idea you had in a hallway conversation turn into a funded product. It has happened enough times now that I have started treating it less as coincidence and more as signal.

Two years ago, I was talking with [Thejpal Ramannagri](https://www.linkedin.com/in/thejpal-ramannagari/) about memory in AI systems. The argument was simple: long-term memory is not something a user should be managing. The agent should own it, evolve it, and improve it without prompting. Today, [Hermes Agent](https://hermes-agent.nousresearch.com/) is gaining traction almost entirely because of this self-improving memory layer. The idea was not novel because it was clever. It was obvious if you were thinking about what agents actually needed to be useful.

Around the same time, [Yash Makkar](https://www.linkedin.com/in/yashmakkar/) wanted to build a tool that turned codebases into visual graphs for developer onboarding. While discussing Hybrid GraphRAG with Neo4j, we landed on something important: codebase data is `semi-structured`. An LLM processing an entire codebase into a knowledge base is expensive and often unnecessary. Agents navigating files through search, grep, and glob patterns are cheaper and more accurate for discovery tasks. Claude Code ships exactly this behaviour. Not a coincidence. Just physics.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">👋 Early versions of Claude Code used RAG + a local vector db, but we found pretty quickly that agentic search generally works better. It is also simpler and doesn’t have the same issues around security, privacy, staleness, and reliability.</p>&mdash; Boris Cherny (@bcherny) <a href="https://twitter.com/bcherny/status/2017824286489383315?ref_src=twsrc%5Etfw">February 1, 2026</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

These two patterns share a common thread: the real unlock was not a better model. It was a better understanding of the problem's shape.

Which brings me to what I think is the next big one.

## The benchmark treadmill

Right now, the AI discourse is stuck in a loop. A new model drops. A new benchmark is cited. Social media fills up with capability demonstrations. Repeat.

<img src="/assets/images/tin-foil-cat-meme.png" style="width: 50%" alt="tinfoil cat meme template">

Nobody is talking about cost per value. OpenClaw, for instance, is doing genuinely interesting work with integrations, but the conversation around it stays focused on what it can do rather than what it costs to do it in production. Nobody is publishing what their agent actually costs to run versus what it is returning. Yes, AI is advancing at a remarkable pace. But for the majority of businesses that are not top-dollar firms with dedicated AI budgets, the unglamorous questions of cost, reliability, and fit are still the ones that determine adoption. The capability gap is shrinking. The integration gap is not.

## The actual moat is distribution

Every major SaaS product right now is bolting AI onto its existing ecosystem. Most are gating it behind a higher tier or a separate membership. This is rational short-term pricing behaviour. It is a long-term adoption trap.

Users do not want another tool. They want their existing tools to get smarter. Look at what Anthropic is doing with Claude: rather than building a monolithic suite, they are taking integrations one at a time. Excel, PowerPoint, and now reportedly Blender. Each integration is a new reason for a different user segment to stay. [n8n](https://n8n.io/) tells the same story from a different angle. It became popular not because it was the most powerful automation tool, but because it became a bridge. Any tool with an API could talk to any other tool. The product did not replace your stack. It connected it. That is why it spread.

![n8n-as-a-bridge: source n8n.io](https://n8niostorageaccount.blob.core.windows.net/n8nio-strapi-blobs-prod/assets/Screenshot_2022_08_05_at_15_05_13_7bb75d8cf5.png)

The products that win will be the ones that integrate horizontally across the workflows users already live in, not the ones selling a new suite they have to migrate to. An AI that lives inside Slack, reads your Notion, checks your calendar, and acts on your behalf without requiring you to open a new tab is not just more convenient. It is structurally stickier. The integration is the lock-in. Not the model. Not the interface.

This is why distribution wins. A good-enough model with excellent integrations beats an excellent model with no integrations, every time.

## Harness engineering is the name for what this requires

![Harness Engineering via X.com](https://pbs.twimg.com/media/HFOWvmAaIAAzGHg?format=jpg&name=900x900)

*Sources:*
- [@akshay_pachaar *via X*](https://x.com/akshay_pachaar/article/2041146899319971922)
- [Vivek Trivedy *via Langchain*](https://www.langchain.com/blog/the-anatomy-of-an-agent-harness)

The industry has recently started using the term "harness engineering" to describe the discipline of building the systems around an AI model: the constraints, the feedback loops, the integrations, the context pipelines. The model is the horse. The harness is everything that makes it go where you need it to go.

This framing correctly relocates the engineering challenge. Think of it this way: the model is the CPU, the harness is the operating system, and the agent is the application. Nobody buys a computer for the CPU alone. The OS is what makes it useful, and the applications are what make it irreplaceable.

Most agent failures in production are not model failures. They are harness failures: broken state management, missing context, tools that do not connect to the right systems. The bottleneck was never the intelligence. It was the infrastructure around it.

Models are becoming interchangeable faster than anyone predicted. The harness is not. And the most defensible part of any harness will be its integrations, how deeply it is woven into the workflows and data sources that users already depend on.

The teams that figure this out first will not just have better products. They will have products that are genuinely hard to replace.

That is the moat. Not the benchmark. Not the context window. The connections.
