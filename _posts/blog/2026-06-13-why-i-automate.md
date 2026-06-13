---
layout: post
title: "Automation: A Personality Disorder"
date: 2026-06-13
tags:
  - automation
  - n8n
  - homelab
  - Luna
description: From a scheduled shutdown script during COVID to a multi-agent home setup, the instinct was always the same. If it is deterministic and repeating, it is a machine's job.
---
![Automate Everything - Meme](https://i.redd.it/6fg3aicn6if41.png)

My mom used to turn the water motor on around 6AM and off around 9AM, then on again around 4:30PM and off by 8:30PM. Part of the routine, never questioned. The problem surfaced when she travelled. She would call me to do it. Every time. I would be in a meeting, debugging a prod build, or elbow-deep in something that actually mattered, the phone would ring, and I would walk to a switch.

I installed an Alexa-enabled IoT switch. The motor runs on a schedule now. We only touch it manually when the WiFi is down, which almost never happens. Every switch in my office is Alexa-controlled. (Home Assistant is on the list, somewhere)

That is the whole philosophy. If something is deterministic and follows a pattern, find a way to let systems talk to each other so you can spend your attention on things that actually require it. Just because you *can* do something does not mean you should be the one doing it every time.

---

## Shortcuts, Not Laziness. Okay, Both.

COVID, 2020. Online labs started @8. I would join, drift off, and wake up still on the call. The professor could see I had been "present" for the entire session.

The fix: a scheduled shutdown [script](https://github.com/thapar25/autoshutdown). Set it before sleeping, PC off mid-session, attendance logged. Not my proudest engineering moment. Entirely effective.

A year later, I wanted a gaming mouse, [Logitech G102](https://amzn.in/d/0emHlTAp), for CSGO but was not going to pay full price. A [scraper](https://github.com/thapar25/webscrapper_raspi) on a Raspberry Pi hit an Amazon URL every morning and sent an email if the price dropped below a threshold. Bought the mouse. Still have it.

Neither of these felt like "automation projects" at the time. They were just solutions to annoyances. In hindsight, the pattern was already there: *find the repetitive part, remove yourself from it*.

---

## Now I Work With Agents

These days that instinct runs through Luna, my personal AI assistant that lives on Slack and orchestrates a growing number of workflows. The backbone of those workflows is n8n.

<img src="/assets/images/luna-x-n8n.png" alt="Luna x n8n" style="width: 60%;" />


If you are thinking about building something similar, whether a full agent setup or just automating the repetitive parts of your personal life, n8n is worth serious consideration. Credential management is painless, integrations exist for almost everything, and you go from idea to running workflow faster than most alternatives. It is not glamorous. It just works, which is the only thing that matters when you are shipping solo.

Here are the five automations that currently earn their keep.

## 1. Infra Alerts to Slack

[[2026-04-27-luna-v2|Luna]] runs on a FastAPI service. n8n handles webhooks and automations. When something breaks, service down, webhook failure, automation error, a Slack alert lands in a dedicated channel.

![Slack Alert Flow](/assets/images/slack-alert-flow.png)

This is the boring one. It is also the one I would set up first if doing it again. Luna already lives on Slack, which means it is already on my phone. Infra alerts in the same place means I am managing my homelab from wherever I am, without opening a dashboard I would never remember to check.

![Slack Alerts](/assets/images/slack-alert-luna.png)


The ambition is a full homelab nerve center in Slack. For now it is alerts. That is enough.

---

## 2. FitBit to Notion Fitness Tracker (11:59PM Daily)

Every night just before midnight, an automation pulls my step count from Google Health and writes it into my Notion fitness tracker.

I do not think about it. I do not open the FitBit app. I do not manually log anything. The data is just there when I want to look at it.

![FitBit Steps Flow](/assets/images/fitbit-steps-workflow.png)

There is more data available from the health API: sleep, heart rate, calories. I only care about steps right now. The automation does exactly that and nothing more. Scope creep is how these things quietly stop working.

---

## 3. OpenRouter Free Tier Model Tracker (Under Development 🚧)

Every day, a job hits an OpenRouter API and checks for new models on the free tier. If any benchmark better than whatever I am currently using as my experimental LLM, a Slack alert arrives suggesting I go try it.

The free tier moves fast. New models drop, benchmarks shift, something genuinely better becomes available and you miss it because you were not watching. This automation watches.

Still being tuned, the benchmark comparison logic needs work, but the premise is solid. Model selection should not require reading release notes.

---

## 4. Mom's Medical Files to Gemini to Report (Under Development 🚧)

My mom emails medical files to a dedicated address. An automation picks them up, passes them to Gemini, and generates a structured `report.md`. The goal is a centralized health record for my parents, everything parsed and stored in one place.

It is unstructured for now. I do not know all the fields I will want yet, so I am not forcing a schema until patterns emerge from the actual data. The ingestion works. The structure will follow.

This one is personal in a way the others are not. There is a full post coming when it is properly built. It deserves more than a section.

---

## 5. Invoice Automation (Delivered)

This one went to a creator friend who was spending several minutes every time she raised an invoice. Pulling brand names, campaign details, amounts, formatting everything correctly, drafting the email. Repetitive, error-prone, tedious. Classic machine work.

![Creator Invoice Details Flow](/assets/images/creator-invoice-details.png)

The automation: emails hit her inbox, an LLM parses them for brand, campaign, amount, and amount-in-words, then prefills a Word template. Before anything is sent, a draft entry appears in her Notion page for review. She checks the values, clicks approve, and a Gmail draft appears ready to send.

![Creator Invoice Review on Notion](/assets/images/creator-invoice-queue.png)

Two minutes saved per invoice does not sound like much. Multiply it across every invoice she raises, add the mental overhead of context-switching into admin mode, and it compounds fast.

![Creator Invoice Draft](/assets/images/creator-email-draft.png)

Human-in-the-loop was a deliberate call here. The machine handles extraction and formatting. The human makes the judgment call before money is involved. That is the right division of labour.

---

## The Throughline

I did not get into automation because I work in AI. I got into it because I was annoyed by a phone call about a water motor.

The tools got better. The scope got larger. The instinct is the same: if it is deterministic, if it is a pattern, if it pulls you away from something that actually needs thinking, find the system, build the connection, get out of the loop.

Luna is where that instinct currently lives. n8n is how most of it gets wired together. There is more being built, including a health agent that will make automation four above look like a warmup.

More on that when it exists.
