---
layout: post
title: Because I'm Batman
date: 2026-09-28
tags:
  - pulse
  - xlr8-labs
  - local-llm
  - personal-ai
description: Founder by day, local models by night, and why the night shift is quietly the roadmap for the day job.
---

![A glowing bat-signal on my desk](/assets/images/bat-signal-desk.jpg)

That's what I feel like. Batman.

By day, Bruce Wayne. Founder, pitches, pleasantries. By night, the work I actually love.

For the past two weeks, the day shift has been a crash course in sales. Leads. Distribution. Vocabulary I had filed under "for MBAs only" is now very much on my plate.

The reason: I started a company. [XLR8 Labs](https://xlr8labs.in/?utm_source=thapar25.github.io&utm_medium=blog&utm_campaign=because-im-batman).

I'd love a pocket deep enough to fund it while I tinker in the cave. That's not how the world works. Somebody has to sell the thing.

## Pulse

We shipped Pulse to a clinic.

It's a clinical dictation tool. The doctor talks, Pulse writes the medical summary, and any follow-up instructions buried in the dictation land on a taskboard for the staff.

<iframe src="https://www.youtube-nocookie.com/embed/vThsBda99vk?rel=0&modestbranding=1&iv_load_policy=3&playsinline=1&fs=0&disablekb=1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Pulse is built to run fully local, on the clinic's own server. This clinic got the hybrid build, because a lot of medical setups in India don't have the hardware to run every model in-house. Transcription stays local. Patient data gets scrubbed before anything leaves the building, and only the clean transcript goes to open-weight cloud models for structuring and reasoning.

Transcription runs on Whisper Large v3. We benchmarked it against Parakeet, Canary and a handful of Nemotron models. Whisper was slower. It was also more accurate, and it was the only one that took a free-text prompt alongside the audio. The NVIDIA models can boost a word list at decode time. That's a nudge. A prompt is context.

That prompt is where it gets personal. Borrowing a trick from [Wispr Flow](https://wisprflow.ai/), Pulse remembers every correction a doctor makes to a note, per doctor. Say the word again and the model already knows it. The medical jargon dictionary behind it came out of lessons from [[2026-06-24-vaid-intro|Vaid]], the health logger I built for my dad.

## Personal AI, Rented

The day shift also means showing up in public. We've started posting on [Twitter](https://x.com/pulkitthapar), demo videos and AI-generated ones. The timing helped. Opus 5.5 landed right when we needed it, and it does a lot with very little instruction.

Sales, though, I'm learning from AI. Literally.

Two Grok bots do the teaching. Rocket Singh handles strategy, and its first lesson was that cold calling doesn't make sense for us today. Joe Goldberg handles prospect research. Very thorough.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">like some of my other agents, the Grok bots are named after pop-culture references.<br><br>yes, the stalker feeds the salesman his leads. <a href="https://t.co/FAXPqwuO6r">pic.twitter.com/FAXPqwuO6r</a></p>- Pulkit Thapar (@pulkitthapar) <a href="https://x.com/pulkitthapar/status/2103459683101237697?ref_src=twsrc%5Etfw">September 25, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>

The third lives in my iMessages. [Instinct](https://instinct.com) has been the talk of the past month, and I've been using it for content ideas and calendars. It works a lot like [[2026-04-27-luna-v2|Luna]]. The difference is that I built Luna. With Instinct, I have no idea which model is answering or how many steps it took to get there. A black box with good manners.

The upside: there's no token cap.

Right now.

## Personal AI, Owned

The night shift is where the fun is.

Lately that means a 27B model running on my own GPU. [Qwen3.8-27B](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF), quantized by IST Austria's DASLab down to IQ2_S. That's 53.8 GB of weights squeezed into 9.3 GB, sitting comfortably on an RTX 4070 Super. On paper it matches the full model on AIME25. In practice, it's good enough to hand real work to.

Two places it earns its keep. The first is deep web search, wired up through a search MCP. The second is small chores on my machine. One Sunday it cleaned out my C drive: stale Docker images and a graveyard of virtual environments. 204 GB, back. The model drove, [pi](https://github.com/earendil-works/pi) was the harness, and I mostly watched.

<blockquote class="twitter-tweet" data-media-max-width="560"><p lang="en" dir="ltr">save your tokens, ask your local models to clean up your C drive. sunday chores, sorted. <a href="https://t.co/x7RXt2CzbM">pic.twitter.com/x7RXt2CzbM</a></p>- Pulkit Thapar (@pulkitthapar) <a href="https://x.com/pulkitthapar/status/2101669251652493332?ref_src=twsrc%5Etfw">September 20, 2026</a></blockquote>

It isn't replacing my Claude subscription. It doesn't need to. What matters is that the subscription is no longer the only way things get done.

## The Night Shift Is the Roadmap

The day job and the night job are the same job.

Pulse runs hybrid today because a clinic server can't hold a capable LLM. Meanwhile, a 27B model is doing chores on a gaming card on my desk. That gap is closing faster than hardware budgets move.

Rented intelligence is great until the terms change. Instinct is free right now. The model on my GPU is mine.

AI is going local. Not all at once. One quantized model at a time.

When the clinic's hardware catches up, Pulse goes fully local. Every night in the cave is practice for that day.

Every Wayne needs an Applied Sciences division. Mine clocks in after dark.
