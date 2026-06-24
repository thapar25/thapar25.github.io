---
layout: post
title: Happy Birthday, You're Onboarded
date: 2026-06-24
tags:
  - ai
  - agents
  - homelab
  - langgraph
  - n8n
  - vaid
description: I built my dad a health-tracking AI agent for his birthday. He didn't get a vote. Here's what's working, what's broken, and why reliability matters more than speed.
---

![Vaid logo](/assets/images/vaid-logo.png)

There's a new agent in the house, ✨***Vaid***✨

V.AI.D. No deep meaning, it just happens to land close to ["वैद"](https://en.wikipedia.org/wiki/Vaidya) *(Sanskrit for a traditional healer)*, and can also be read as ["वेद"](https://hi.wikipedia.org/wiki/%E0%A4%B5%E0%A5%87%E0%A4%A6), the word for sacred texts, reads fine as Virtual AID too. I'll take a name that works on multiple levels by accident over one I spent a week overthinking.

I gave it to my dad for his birthday. Happy birthday, you're onboarded. He did not get a vote.

## Why Vaid exists

My dad has [CKD](https://en.wikipedia.org/wiki/Chronic_kidney_disease). Chronic kidney disease means routine blood pressure checks, lab reports, and a level of tracking that doesn't fit neatly into a notes app you open twice a week.

He runs his life on Excel sheets. I run mine on Notion. I was not about to make my dad relearn how he tracks his own health, so I did not bring him over to Luna's stack. I wrote tools that append directly to his Excel sheet instead.

## The bones, borrowed from Luna

If you've read about [[2026-04-27-luna-v2|Luna]], most of this will look familiar. Same underlying architecture, repointed at a different problem.

An iPhone shortcut captures voice input, `Whisper STT` transcribes it, and `Groq` running `gpt-oss` handles the reasoning. `FastAPI` and `LangGraph` run the orchestration, with header auth keeping it locked down. `n8n` handles webhooks and monitoring, and `Jaeger` plus `LangSmith` give me the same observability stack I leaned on for Luna. Slack channels for error alerts has become my go-to.

The pattern holds: build the nerve center once, then point it at whatever problem needs a nervous system next.

## What's working today

- **`log_health_metrics`**: logs one or more quantitative readings from a single sentence, no follow-up questions, with Indian units assumed by default (kg, mmHg, mg/dL, and so on)
- **`log_meal`**: logs meals and drinks from vague descriptions, estimating calories and macros itself instead of asking you to weigh anything
- **`log_health_note`**: captures qualitative observations, mood, symptoms, sleep quality, in your own words, structured later downstream

![LangSmith trace for a Vaid run](/assets/images/vaid-langsmith-bp-trace.png)

BP tracking, morning and evening, is solid. My dad talks, Vaid logs it, the friction that used to make him skip a reading is gone. Here's the sheet it lands in:

![Dad's BP tracking Excel sheet](/assets/images/vaid-excel-sheet.png)

That's the whole point. He still opens the same Excel file he always has. He just never has to type into it himself. Meal tracking exists for the same reason BP tracking does, my **parents undersell their own protein intake** and I wanted real numbers instead of 'we eat fine.' My dad took one look at the feature and recognized it for what it actually is: a body camera for his snacking, with my mom as the department reviewing the footage.

Behind it, the same stack from Luna is doing its job:

![n8n workflow powering Vaid](/assets/images/vaid-tools-n8n-flows.png)

It's also technically capable of meal tracking. He's a foodie. `He would never.`

## The part that isn't solved yet 🚧

Here's where this stops being a victory lap and starts being an actual build log.

My parents forward lab reports to a dedicated mailbox. Vaid is supposed to parse them, extract the numbers, and structure the data. In testing, this is the part that keeps finding new ways to break.

Some labs hand back graphic PDFs instead of clean text, the kind that look fine to a human eye and like noise to a parser. Other times, two or three separate reports get bundled into a single file, and figuring out where one ends and the next begins is its own small research problem. I'm running this against Gemini vision, on the free tier, which adds a third constraint on top of the first two: reliability that doesn't cost anything.

None of this is exotic engineering. It's just the unglamorous reality of structured extraction from documents that were never designed to be machine-readable. Worth saying plainly, because most "AI parses your documents" posts skip this part entirely.

## Why I'm not shipping this until it's boring

This is health data for two people who trust me to get it right. A wrong BP reading is annoying. A wrong lab value, silently logged as correct, is a different category of problem.

So alongside the parsing work, I'm building scheduled evals that compare what the user actually said against what Vaid recorded, specifically to catch discrepancies before they become someone's medical record. These run offline, using Gemma 4 on my Ollama setup, which has turned into a genuinely fun side project in its own right.

The goal is a system boring enough to trust without checking.

## What's next

Apple Watch integration for richer health signals, a parsing pipeline that survives contact with real-world lab PDFs, and an eval loop that runs quietly in the background until I have a reason to look at it.

Unlike Fitbit data for [[2026-06-13-why-i-automate|Luna's fitness tracker]], Apple Health data is a different story.  

Vaid, like the word it borrows from, is meant to heal quietly in the background. Right now it's still in the apprentice stage. I'll write the next one once it's earned the title.
