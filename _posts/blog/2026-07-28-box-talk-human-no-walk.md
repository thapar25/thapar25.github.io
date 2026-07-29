---
layout: post
title: Box Talk. Human No Walk
date: 2026-07-28
tags:
  - reverse-engineering
  - ai-for-all
description: A legacy fuel station box that wouldn't stay on the network, why vendor lock-in made it that way, and how a laptop-side hack got us talking to it without touching a thing.
---

![Access Denied Meme](/assets/images/access-denied.png)

Somewhere in the middle of debugging a dead connection, I made the mistake of asking Claude for a caveman translation of the whole ordeal. It refused to leave my head.

![Claude's caveman translation of the network fix](/assets/images/box-talk-caveman-screenshot.png)

So the section titles in this post talk caveman too. Fair warning: what follows is some genuinely fiddly networking and reconciliation engineering, described using the smallest words available, entirely on purpose.

One housekeeping note before this goes further, every "we" past this point means Claude and I.

## Big Guy Own Box.

For years, automated fuel stations across India have run on the same arrangement. The software running the pumps and tanks belongs to the company, not the dealer standing on site every day.

My dad's automation system came from a payment vendor, sold to the company as part of the deal, then installed at his station. It reports up. It reconciles for corporate. Nobody built it to give the dealer a one-shot bird's-eye view of their own site.

The software works exactly as designed. It just wasn't designed for the person running the place.

## Look, No Touch.

The box itself runs Linux. PHP and SQLite underneath, a JSON-RPC layer on top, the kind of stack that looks intimidating until you've spent enough weekends poking around your own [[2026-04-11-immich|homelab]].

That's the part that transferred directly. Months of SSH-ing into machines that weren't mine to break gave me the [[2026-06-13-why-i-automate|instinct]] for this one too: look everywhere, touch nothing. Claude Code helped map the filesystem, find the database, work out what each table actually held.

Every query built from here reads. None of them write. The box keeps doing exactly what it was doing before we showed up. We just started listening in.

## Wifi Weak. Human Walk Every Day. Grr.

Reading the box meant reaching the box, and reaching it was the actual fight.

It ran on its own SIM module, could connect to Wi-Fi, but the enterprise hardware's power-saving mode kept dropping the connection overnight. Every morning, someone had to physically walk over and reconnect it before anything downstream could even start.

That's not a system. That's a chore with extra steps.

## Box Talk. Human No Walk.

The fix seemed obvious: stop relying on Wi-Fi. A Wi-Fi repeater *doubling as a receiver* had a spare Ethernet port, so we ran a cable from that into the box's Ethernet port instead. Wired, stable, no more overnight drops.

![Subnet Mismatch](/assets/images/subnet-mismatch.png)

Except the box still wouldn't talk. It had a **static IP** left over from an old point-to-point link to a different sensor-display setup, on a subnet that didn't match the network actually running through that cable. Same wire, two different addresses. Neither side ever said a word to the other.

We couldn't fix it on the box's end. No sudo, and that same static config was still quietly serving something else we didn't want to break. Reconfiguring it directly was off the table, same rule as always: look, don't touch.

So we moved the fix to our side instead. Gave a laptop a second IP, an alias sitting inside the box's old subnet, right alongside its normal address on the real network. Same wire, now speaking the same language on both ends. The handshake went through on the first try.

![Problem Statement](/assets/images/bos-box-problem-statement.png)

No changes to the box. Fully reversible. **Box talk, human no walk.**

## Box Get Eyes. Dad See Everything. Yay.

Once the box actually answered, we built a Streamlit dashboard that connects over SSH, opens a tunnel for the box's own JSON-RPC calls, and pulls live data straight from the db.

Don't even get me started, I'm already three agents deep in my head on what this feed could produce (happy Pulkit giggles).

![Dashboard](/assets/images/tank-status.png)

Four tanks, live volume, temperature, ullage, one glance.

![Site Map](/assets/images/site-map.png)

The forecourt mini-map mirrors the physical layout of the site, island by island, product by product, so my dad recognizes it instantly without a legend.

It's a real system, running against a real box, at a real site. It's also still a POC. Single session, no history backfill, and the physical register employees use for manual sale math is still very much alive on the counter. 

## More Box Come. Human No Rush.

The physical register dies once the next piece lands: printed template sheets, an office printer doing double duty as a scanner, a local vision model reading handwritten entries straight into the same Excel sheet my dad already checks. Design stage only, nothing built yet.

Beyond that: attendance, radio reporting over the walkie-talkies already sitting at the site, agent co-pilots surfacing alerts for the numbers my dad actually cares about. Each one gets a line here and nothing more. The rest stays unbuilt on purpose.

It would be easy to point every piece of hardware in the home lab at this station and call it progress. That's not the goal. One piece of failed tech shouldn't be able to take down a working fuel station.

So the plan is coexistence, not a flip of a switch. Old system and new system running side by side for a few months, until the numbers do the convincing on their own. 

My dad is the hardest client I've ever had. He'll switch when the math tells him to, not before.
