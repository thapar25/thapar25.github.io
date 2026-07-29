---
layout: post
title: "My Second Favourite Spider-Man Line"
date: 2026-07-24
tags: [ai, india, voice-ai, dost-ai, building-in-public]
description: "Building a voice-first AI for people the internet forgot"
---

Everyone knows the first one.

> With great power comes great responsibility. 

My second favorite line hits differently.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">&quot;When you can do the things that I can, but you don&#39;t, and then the bad things happen, they happen because of you.&quot; –Spider-Man, Captain America: Civil War</p>&mdash; Disney (@Disney) <a href="https://x.com/Disney/status/1227313856973811713?ref_src=twsrc%5Etfw">February 11, 2020</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>

I think about that line every time I build.

---
## The gap nobody's pricing in

![The street vendor scene from 3 Idiots: asked for an address, he can't read it but talks his way through anyway](/assets/images/3-idiots-vendor-collage.png)

There's this scene in 3 Idiots where a street vendor is asked for directions. He can't read the address. He can talk just fine.

That's the entire population most AI products quietly write off. Not because the technology can't reach them, but because reaching them was never the business case.

Every major voice and language model on the planet is trained, tuned, and benchmarked for English and a handful of Latin-script languages first. Indian dialects show up eventually, if at all, as an afterthought bolted onto a roadmap slide. Companies are absolutely solving voice AI. They're solving it for businesses that can pay for it, not for the people who need it most.

There's no B2B contract sitting on the other side of someone asking a phone what to do about a stomach ache in a language no assistant bothers to learn. So nobody builds for them. ***The market doesn't reward it, so the market doesn't show up.***

## What Dost.AI actually does

Dost.AI is a React Native Android app, built voice first because voice is the one interface *almost* everyone already knows how to use, regardless of whether they ever learned to read a screen.

![Dost AI Demo](/assets/images/dost-demo.gif)

Under the hood it's an STT-LLM-TTS sandwich, and every layer is deliberately provider-agnostic. I didn't want a single voice vendor's outage or price hike to take the whole thing down.

![STT-TTS Sandwich](/assets/images/stt-llm-tts.png)

[Sarvam AI](https://www.sarvam.ai/) handles speech-to-text and text-to-speech, and their work on Indian languages is genuinely exceptional, better than anything else I tested for this use case. [Groq](https://groq.com/)'s gpt-oss 120B model handles the reasoning layer, running free tier. The whole thing runs on `Oracle's free tier` for hosting.

The app uses location services to set a default language automatically. Right now Punjabi and Marathi are the two dialects actually live and in use, spreading through me and my uncle handing out APKs to whoever's willing to try it.

<img src="/assets/images/dost-location-services-permission.png" alt="Dost Location Services" style="max-width: 280px;">

## The pilot is smaller than you'd think, and that's the point

I've given the APK to two people outside my own testing circle so far.

Mr. Panjab Singh, in his sixties, moved to a touchscreen phone about a year ago, and he's still adjusting to the device itself, let alone the app. He hasn't really started using it yet, and that's a data point too. Voice-first only works if someone can get comfortable holding a smartphone in the first place.

Our domestic help has used it more, four or five conversations so far, mostly asking word meanings and questions about government pension schemes. Not financial advice, just what the terms actually mean. Some days she asks her kids instead, which tells me something about trust and habit that no amount of engineering fixes on its own.

A couple of people have asked about current affairs. Since there's no web search built in yet, Dost.AI says it doesn't know rather than making something up. I'd rather it admit ignorance than hallucinate a confident wrong answer to someone who has no way of fact checking it.

I'm still looking for the person this was actually built for. Two users and a handful of honest conversations is where this stands today, and I'd rather say that plainly than dress it up.

## Why this stays a pilot for now

There's no Play Store listing, and that's intentional. Firebase is already wired in for OTP verification, but I'm not turning it on yet, because I don't want to absorb that cost or the legal overhead of a public listing before I know this actually works for the people it's meant for.

The build still has observability baked in for now, purely so I can debug and understand where people get stuck. The finished version won't have any of that. People asking a phone about their pension or their symptoms deserve privacy, not a debug log with their conversations in it.

This is also entirely self-funded, out of my own pocket, with no job backing it anymore. `Google will probably ship something like this natively into Gemini and Android eventually.` Until they do, I'm building the version that exists today instead of waiting for the one that might exist later.

## Where this could go

There's a bigger version of Dost.AI sitting in my notes right now, one where the same voice-first interface plugs directly into the systems people already need to deal with, banks, hospitals, government offices, without ever asking them to read a form. I'm not ready to lay out how yet. Some ideas need to stay half built before they're worth saying out loud.

There's also a harder problem I'm circling, one nobody in India is seriously solving today: how doctor-patient conversations turn into records that actually get maintained, done locally instead of shipped off to someone else's cloud. I don't know exactly what that looks like yet. I'm fairly confident it matters a lot more than it looks like it does right now, probably within the next three or four years.

## The actual hot take

> Take the money out of tech and watch how many founders are still standing there wanting to solve problems.

Watch how many developers are too, because this isn't just a founder problem, it's a herd mentality problem, *bhedchaal*, and there's no clean English word for how well that captures it.

This isn't building toward something that eventually raises a round and serves the top slice of people who can already afford every tool that exists. I wanted to contribute something back, to people the industry has quietly decided aren't worth building for.

## Back to the beginning

Voice was never a technical choice for Dost.AI. It was the only honest one. Someone who was never taught to read English, or type a search query, or navigate an app built by and for people who took all of that for granted, still has a voice, and still has questions worth answering.

Powered by Groq and Sarvam. AI4Bharat is next, for the healthcare direction I mentioned above. Different build, same conviction: the tools exist, somebody just has to point them at the people who've been left out of the room.

Bad things happen because of you. So do the good ones. I'd rather spend my time on the second half of that sentence.
