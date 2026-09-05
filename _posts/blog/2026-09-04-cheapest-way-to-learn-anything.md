---
layout: post
title: The Cheapest Way to Learn Anything
date: 2026-09-04
tags:
  - two-cents
  - AI
  - learning
description: Negatives, LangChain docs, and why the gaps documentation leaves open teach you more than any course ever will.
---

![Karate Kid wax on wax off](/assets/images/karate-kid-wax-on-wax-off.png)

Mr. Miyagi never explained wax on, wax off.

Daniel-san just did it. Hundreds of reps, understanding arriving weeks later, uninvited, already fully formed in his arms.

I learned the same lesson from [Chris Heria](https://www.youtube.com/chrisheria), minus the bonsai trees. 

I couldn't do a single one. Chris had a fix for that: **negatives**. Jump to the top of the bar, then fight the drop down as slowly as your arms allow. Week one, I could barely control the first three inches. Week two, something clicked, and I pulled my own bodyweight up for the first time in my life.

Nobody taught me the pull-up. My arms just ran the rep enough times that the rep became possible.

## The Theory

That's the whole theory, really. **Negatives.**

You don't start with the part you can't do. You start with the part you can barely control, and you let your body catch up to the rep before your brain understands why it works.

There's a gym bro term for it. **Eccentric training**. Turns out I'd stumbled into something with an actual name.

Learning works the same way. You don't start with the part you can't explain. You start with the part you can barely follow, code you copy without understanding, a doc you skim twice, and you let your understanding catch up to the rep before your brain demands the theory.

I didn't know any of that hanging off a bar in week one. I just knew the drop worked. Everything after that, LangChain, voice AI, design, has been the same drop, over and over, in different gyms.

## 2023, LangChain, No Idea What I Was Doing

I had no idea what an LLM was. No idea what OpenAI's API did, no idea what a vector database was for. I just wanted to build a chatbot that could answer questions from my own documents.

So I opened LangChain's documentation and started copying code.

I didn't read it top to bottom like a textbook. I grabbed a snippet, ran it, watched it break, read the error, fixed it, ran it again. Half the time I didn't know what a line did until I deleted it and watched something stop working.

That's how I learned what a vector database actually was. Not from a definition. From noticing a `.chroma` directory spawn in my codebase and going down a rabbit hole to figure out what it was and why it was there.

By the end of it I'd built a working RAG chatbot and picked up an entire vocabulary I couldn't have defined a week earlier. **Embeddings, retrieval, chunking, context windows.** None of it came from a lecture. All of it came from the drop.

## Same Drop, Different Gyms

Voice AI and speech recognition, I'm reading through [Pipecat's documentation](https://docs.pipecat.ai/), the actual framework people building voice agents run on, not a course explaining voice AI at a surface level. Marketing, [HubSpot's own docs](https://developers.hubspot.com/docs) instead of a marketing masterclass. Design, [[2026-08-19-i-design|I wrote about this one already]], Paper Design, [Hyperframes](https://hyperframes.heygen.com/developers/overview), Next.js, the actual tools' docs instead of a UI/UX bootcamp.

You're not supposed to fully understand it on the first pass. You're supposed to *survive the first pass*.

I'm three drops into this one and I still can't tell you the theory behind a diffusion-based TTS model. I can tell you it exists, I can tell you which parameter I broke it with, and I can tell you what it sounded like when it worked.

## Courses Teach the Space. Docs Lead It.

![Kermit Python Course Meme](/assets/images/kermit-python-course-meme.png)

Here's the pattern I keep seeing. Someone wants to learn a new skill, and the first thing they search for is a course, before documentation, before the source.

I'm not throwing shade. I get the appeal, a course promises a shortcut, a curriculum, someone else doing the hard part of figuring out what matters. But a course is built by someone **teaching** the space. Documentation is written by someone **leading** it.

Those are not the same person, and they are rarely even in the same room. A course author is optimizing for clarity and completion rates, a finished product for an audience that wants to feel like they learned something in three days. The people who wrote LangChain's docs, HubSpot's docs, Pipecat's docs, they're not teaching, they're just showing you the thing they built, exactly as it is, gaps and all.

The gaps are the part that teaches you. A course fills every gap before you notice it's there, hands you a finished thought and calls it a lesson. Documentation just leaves the gap open and walks away.

Standing in that gap, you're forced to think your own thought. What does this parameter actually do. Why did this break. What is this library assuming I already know. Nobody's thought reaches you first, so the thought you end up with is yours, built from your own confusion instead of borrowed from someone else's slide deck.

That's the actual difference. A course hands you a thought to carry. Documentation makes you build one, and you get to keep it, because you're the one who made it.

🚨 None of this is free, to be clear. The price is **your time**, hours you could've spent watching someone else explain it faster. But time was always the actual currency. Everything else was just packaging.
