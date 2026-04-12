---
layout: post
title: The Friction Is the Feature (You're Fighting)
date: 2026-04-12
tags:
  - Luna
  - AI
  - homelab
  - personal-assistant
  - ios-shortcuts
description: Building a habit tracker is easy. Actually using it isn't. Here's how I removed the friction entirely, and why a two-tap lock screen button beat a native app.
---

<div class="tenor-gif-embed" data-postid="18002448761037760173" data-share-method="host" data-aspect-ratio="1.33333" data-width="100%"><a href="https://tenor.com/view/louis-litt-litt-litt-up-suits-gif-18002448761037760173">Louis Litt Litt Up GIF</a>from <a href="https://tenor.com/search/louis+litt-gifs">Louis Litt GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>
<br><br>

[Louis Litt](https://suits.fandom.com/wiki/Louis_Litt) carried a Dictaphone everywhere. Barked memos into it mid-stride, never broke his pace, never got distracted. It always seemed a little ridiculous.

I get it now.

---

Every habit tracker fails the same way.

Not because it's badly built. Because it requires you to open it. You finish a workout, tell yourself you'll log it later, and later never comes. The app becomes a graveyard of good intentions. The data gap is not a discipline problem. It's a friction problem.

This is what I was trying to solve with Luna.

## What Luna actually does (the short version)
Luna is my personal AI assistant: a [LangGraph](https://langchain-ai.github.io/langgraph/) multi-agent system and [n8n](https://n8n.io/) automation flows, all running on my homelab, wired into my Notion workspace and Google Calendar (for now). One name, one interface, for everything.

This post is about the front door: an [iPhone Shortcut](https://support.apple.com/en-in/guide/shortcuts/welcome/ios).

## The constraint that made the decision easy

Luna runs on my homelab, exposed to the outside world via a [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/). That means REST API: clean, simple, battle-tested. What it doesn't give me is a persistent duplex connection. WebSocket is off the table for now. So a native app with any kind of real-time feel would've been more work for a worse result. Shortcuts talking to a REST endpoint is the honest architecture for the setup I have.

I'll build a proper app when it makes sense. Right now, it doesn't.

## Two shortcuts, one idea

There are two shortcuts doing the work.

The first lives on my lock screen and in the notification center. One tap. It records my voice, sends the audio to [Groq's Whisper API](https://console.groq.com/docs/speech-text) for transcription, and fires the text to Luna's backend. I never unlock the phone. I never see a feed. The job is done before the algorithm gets a chance.

The second is called **"Ask Luna"**, completely hands-free. Say *"Hey Siri, Ask Luna"* and it runs. This one uses on-device ASR instead of Whisper, so the accuracy isn't as sharp, but it works well enough when I'm driving or my hands are full.

A Dictaphone. With a backend.

## The actual problem it solves

Think about every app that asks you to manually enter information: fitness logs, food diaries, task managers, journals. The input step is where they all die. By the time you've unlocked your phone, navigated to the right screen, and tapped into a text field, you're already two notifications deep into something else.

Voice-to-lock-screen cuts all of that out. I finish a set, tap once, say "12 pull-ups, ate clean today," and move on. That goes into my Notion Fitness Tracker. No app open, no feed in my peripheral vision, no "I'll do it later."

Same for tasks: *"Add a note to read [Hackers and Painters](https://paulgraham.com/hackpaint.html) by Paul Graham"* lands in my Hobby Projects board. Scheduling requests go to Donna, my calendar agent. Luna routes everything.

## Luna isn't a chatbot
This is worth saying clearly: Luna isn't designed for conversation. The priority is to get things done, not generate replies.

When I log a workout, I don't *need* an acknowledgement. When I create a task, I don't *need* it read back to me. The shortcut fires, the agent acts, and my phone reads the response back to me via TTS when there's something worth saying. Most interactions are still fire-and-forget, Luna confirms a task was logged, tells me my next meeting, answers a question. No screen required. The async model isn't a limitation. It's the point.

## What's next

The next post covers the backend: how I'm running a full multi-agent system at near-zero cost by distributing across LLM providers. [Groq](https://groq.com) for routing, [OpenRouter](https://openrouter.ai) with round-robin key rotation for agents, [Gemini](https://deepmind.google/models/gemini/) as fallback. Plus caching, tool calls, and the feedback loop I'm using to improve Luna over time.

The shortcut is intentionally dumb. The backend is where it gets interesting.
