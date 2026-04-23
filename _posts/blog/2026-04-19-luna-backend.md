---
layout: post
title: "The Underdog Stack: How Luna Runs on Free Inference"
date: 2026-04-19
tags:
  - Luna
  - AI
  - homelab
  - personal-assistant
  - LangGraph
description: Luna is being rebuilt. Here is what is running under the hood right now, why a Chinese MoE model nobody talks about is doing the heavy lifting, and why the next version fixes a problem the current one cannot.
---

![The Donna Device from Suits](/assets/images/the-donna.png)

If you've watched Suits, you already get it. [(incase you're uncultured)](https://chat.openai.com/?q=what+is+the+Donna+device+from+Suits)

I wanted that. Something omnipresent, anticipatory, works across every context. I called it **Luna** instead of The Donna because the vision was never just one interface. A shortcut, a WhatsApp message, a Slack command, an n8n automation. Same brain, different doors.

The [[2026-04-12-luna-ios-shortcut|last post]] covered the front door: an iOS shortcut on my lock screen, one tap, voice memo fired into a backend. This post is about what is behind that door, what it actually runs on, and why I am rebuilding it before adding anything new.

---

## The Architecture (Right Now)

![Luna AI Graph as Mermaid Chart](/assets/svgs/mermaid-diagram-2026-04-19T21-47-58.svg)

Luna is a [LangGraph](https://langchain-ai.github.io/langgraph/) multi-agent system. Every message comes in, gets loaded with chat history from Redis, and hits a router. The router classifies intent and fires to one of four agents:

- **Notion agent**: reads and writes to my workspace. Tasks, projects, fitness logs, notes.
- **Calendar agent (Donna)**: manages Google Calendar. Scheduling, busy slots, edits, removals.
- **Fitness tracker (Rocky)**: dedicated logging agent for workouts and activity.
- **General agent**: everything else. Q&A, quick lookups, conversations.

Each agent runs its tools, returns a response, and the result gets pushed back to Redis with the updated conversation history. Clean, stateless agents. Stateful conversations.

<img src="/assets/images/langsmith-dashboard-tools.png" style="border-radius: 10px;" alt="Langsmith Dashboard for Tools">

The observability and feedback loops are taken care of via [Langsmith](https://smith.langchain.com/) (more about this, in a later post).

That is the current version. It works. And it has one problem.


## Where It Breaks

Say you tell Luna: *"Add a task to check out Wan2.2 and block two hours for it on Friday, after work."*

One sentence. Two agents. Right now the router picks one and sends it there. The Notion agent creates the task. The calendar block never happens. Or vice versa.

The routing is a single `match` statement. One task, one destination. No mechanism for agents to talk to each other, no fan-out for overlapping intent, no synthesis layer for dual-delegation.

Usage data made this obvious. It kept showing up in the logs. Luna v2 fixes this: the router identifies multi-agent tasks, dispatches to multiple nodes in parallel, and synthesizes a single response. LangGraph supports it. The current graph just does not use it yet.

## The Underdog Stack

Luna runs on a repurposed college laptop. Ubuntu, homelab, Cloudflare Tunnel. Infrastructure cost: electricity. API cost: close to zero.

**[Groq](https://groq.com)** runs three jobs. [Whisper](https://console.groq.com/docs/model/whisper-large-v3) handles transcription. The router uses [gpt-oss-20b](https://console.groq.com/docs/model/openai/gpt-oss-20b) with structured output and strict mode for fast, reliable intent classification. The lightweight agents (general Q&A, calendar, fitness) also run on [gpt-oss-120b](https://console.groq.com/docs/model/openai/gpt-oss-120b). Fast enough to feel instant. Free tier covers everything at personal usage volumes.

**[GLM-4.5 Air by Z-AI](https://openrouter.ai/z-ai/glm-4.5-air:free)** handles the heavy Notion agent. Ten tools, full datasource context, real read-write operations against my workspace. Purpose-built for agentic applications, MoE architecture, 131K context window, and a thinking/non-thinking toggle depending on whether the flow needs reasoning or just speed. Reasoning is explicitly turned off in the Notion agent config. For tool-calling flows you want decisiveness, not deliberation. A Chinese lab's open-source model is running the most critical part of this system for free. That is worth saying out loud.

Before GLM-4.5 Air, this slot was **[Step 3.5 Flash by StepFun](https://openrouter.ai/stepfun/step-3.5-flash:free)** (really slept on, in my opinion). 196 billion total parameters with only 11 billion active per token via sparse MoE. Multi-Token Prediction generating 4 tokens per forward pass, hitting 100 to 300 tokens per second in typical usage. It reasoned like a large model and moved like a small one. The free tier on OpenRouter dried up last month. GLM stepped in and has not missed a beat.

Both of these models come from labs that do not get the coverage they deserve. If you are building anything agentic and have not looked at either of them, you should.

Four OpenRouter API keys rotate automatically via a `KeyRotator`. When one hits a rate limit, the next one picks up. Rate limits per key become irrelevant at personal usage volumes.

**[Gemini](https://deepmind.google/models/gemini/)** sits at the bottom via `ModelFallbackMiddleware`. GLM fails, Gemini catches it. Gemini fails, Groq catches it. Three layers of free inference before a single rupee gets spent.

This is not cheapness. It is a deliberate tiered inference strategy. Fast model for routing, capable free model for heavy tool use, two fallback layers below it.

We call that the finest form of [_**Jugaad**_](https://en.wikipedia.org/wiki/Jugaad)

## What Is Next

Luna v2 is the immediate priority: rewire tools, multi-agent dispatch, inter-agent communication, proper handling of tasks that span multiple domains.

After that: a WhatsApp interface already [in progress](https://www.linkedin.com/posts/pulkit-thapar_ambientagents-selfhost-homelab-activity-7404026765439950849-ydaJ), then Slack, then the n8n automation layer expanding significantly. Same brain. More doors.

The shortcut was always the starting point. The architecture has to be built for omnipresence before any new interface gets added.

The brain comes first. The ears come later.