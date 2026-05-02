---
layout: post
title: I Smell The 3D Printer Coming
date: 2026-05-02
tags:
  - blender
  - 3d-printing
  - mcp
  - AI
description: A rough render, a real unlock, and one step closer to buying a 3D printer.
---

There is a pattern I have noticed with myself. The moment I save enough money to feel comfortable, something finds me. Something I want but cannot fully justify.

Right now, that something is a 3D printer.

A few months ago, [TRELLIS 2](https://microsoft.github.io/TRELLIS.2/) made it worse. Microsoft dropped a 4 billion parameter model that takes a single image and spits out a fully textured 3D asset in seconds.

<video autoplay loop muted playsinline aria-label="Trellis 2 via Microsoft" style="width:70%;">
<source src="https://microsoft.github.io/TRELLIS.2/assets/reconstruction/retro_fridge_tv.mp4" type="video/mp4">
</video>


<br>

I watched the demo, raised an eyebrow, and quietly moved the 3D printer a little higher on my wishlist.

Then this week I did something dumber and more interesting.

I gave Claude a photo of my desk and asked it to build a 3D model in [Blender via MCP](https://www.blender.org/lab/mcp-server/). 

![Claude Chat Screenshot](/assets/images/claude-blender-mcp-chat.jpg)

![Animation rendered via Blender MCP + Claude](/assets/images/blender-mcp-output.gif)

Not perfect. But it rendered.

*One thing worth mentioning for anyone trying this: if Claude and Blender are on separate machines, MCP's default `stdio` won't cut it. Switch to `http` and expose it over your local network.*

Here is the thing about the 3D printer sitting in my wishlist for years: the barrier was never the money. It was the time. Learning 3D modeling always felt like a full commitment I could not justify. TRELLIS showed me the ceiling of what AI can do here. Blender MCP gave me something more valuable: a starting point I could actually own.

That distinction matters. One does the work for you. The other teaches you how the work gets done.

AI is not here to kill the skill. It is here to hand you the door. You still have to walk through it.

Anyway. Now I know what no-code CEOs felt shipping their first website.

> The 3D printer is getting closer ;)
