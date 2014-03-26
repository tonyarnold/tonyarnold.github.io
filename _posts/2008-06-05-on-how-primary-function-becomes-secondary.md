---
layout: post
title: On how primary function becomes secondary
tags: [Hyperspaces, Mac]
date: 05 June 2008 01:35:00
---

Over the last month, I’ve been slowly expanding my list of testers who are helping me with [Hyperspaces][1]. Initially, most of the testers viewed [Hyperspaces][1] as a novelty (which it is), but didn’t leave it running. They’d test whether a new build worked, and then go back to what they were doing. It was an interesting thing to watch: I’d poured months and months of my time into making the visual space switcher function properly, and nobody was really using it.

*   Does it show a near real-time overview of what’s happening on all of your spaces? **Check.**
*   Does it use nearly no CPU? **Check.**
*   Does it look good? myyeeeeah - **it’s not terrible.**

Initially, I didn’t pay much attention to what was happening here, and just plowed through adding in some of what I considered to be secondary features. This included the ability to set a different desktop image, a tinted colour overlay and text labels on each of your spaces.

It turns out I was seriously off-base with what people actually miss from [VirtueDesktops][2] and it’s ilk. The big ticket item that seems to be missing from Apple’s implementation with Spaces is context: **Which space am I currently working in?**

Anyhow, those are just my observations - don’t assume that you know what’s important based solely upon your own experience and ideas. In my case, this wasn’t time lost or wasted - the technical work involved in gathering information about how Spaces works is used just about everywhere in [Hyperspaces][1], and once I’ve released the app, I’ll share a lot of what I’ve learned so that others can benefit from that research.

Now before [Neil][3] has a go at me for not releasing a public beta before [WWDC][4] - because apparently he’s not too keen on attending with a “has been” - I am serious about getting [Hyperspaces][1] into your hands as soon as I can, but I’m not going to release something that is **almost** good enough. I’m almost there, and you can help me - I’m about to build the final visuals for the switcher, and I’d appreciate some feedback.

Here’s how it looks in 1.0 alpha build 404 (heh - yes, I see it too):

<img src="http://static.tonyarnold.com/switcher_now.png" alt="Current Hyperspaces switcher" class="center"/>

It functions much as you’d expect - you click on a space to switch to it. The active space shows a live-updating image of your current space, and the others show ghosted representations of your windows. Everything is drawn using CoreAnimation, so transitions of window positions smoothly fade in and out as window positions change on other spaces.

Here are my rough ideas mocked up using Fireworks for where this is could head:

## The QuickSilver concept

The first is a QuickSilver-style window that would include other functionality and configuration options:

<img src="http://static.tonyarnold.com/idea_window.png" alt="QuickSilver-style switcher idea" class="center"/>

## The HUD concept

The second (and my current front-runner with a bit more polish) is this black, hud-like window. It also reflects some of the design elements of Hyperspaces very, very unique icon which I’ll be introducing before the week is out.

<img src="http://static.tonyarnold.com/idea_black.png" alt="HUD-style switcher idea" class="center"/>

Leave your thoughts in the comments.

 [1]: http://hyperspacesapp.com/
 [2]: http://virtuedesktops.info/
 [3]: http://neilang.com/
 [4]: http://developer.apple.com/wwdc/
