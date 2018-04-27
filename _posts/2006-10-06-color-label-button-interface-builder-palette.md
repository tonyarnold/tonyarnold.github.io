---
layout: post
title: Color Label Button Interface Builder Palette
tags: [Cocoa, Programming]
date: 06 October 2006 06:30:00
---

{% capture years_ago %}{{ site.time | date: "%Y" | minus:2005 }}{% endcapture %}

> ## Outdated Info
> Hi there! So it's the future now ({{site.time | date: "%Y"}} to be precise) and things have moved on: Interface Builder Plugins aren't possible anymore, so this post is just a wonderful curiosity.

So [VirtueDesktops][1] has a small problem in that when it was written, Cocoa Bindings were new and not as well understood as they are now. Lately, I’ve been spending a my time brushing up my understanding of basic cocoa concepts that I may have missed first go around. Below is the result of that brushing, and something that I think is drastically under utilised - custom Interface Builder (IB) palettes.

<img src="http://static.tonyarnold.com/color_label-1306152068.png" alt="ColorLabelButtonImage" class="center"/>

[VirtueDesktops][1] has the concept of “labelling” your desktops, much like you label files in the Finder. Given how used to the existing UI users are, representing it in the same fashion in the [VirtueDesktops][1] UI seems entirely logical to me. Surprise, surprise, this is one of those wonderful custom UI elements that Apple is so damned famous for not opening to developers (and in this case, I can understand given how little it is used elsewhere). So what do you do in a situation like this?

Thomas (the original author of [VirtueDesktops][1]), made a custom subclass of the NSControl and NSActionCell cocoa classes, and hooked this into a view programmatically. It worked well (and is still present in the current release of [VirtueDesktops][1]), and for all intents and purposes is a completely valid approach to the problem. Unfortunately, it has the side effect of swizzling view code (in the MVC sense) into places I don’t think view code belongs. And I can’t use IB to nicely manage every aspect of my UI (which is idealistic, but possible).

Here’s my approach: For custom controls like this, I’m writing them into a simple, reusable framework and IB palette. This way, I can make my actual code a lot, lot simpler which has the flow on effect of making it easier to find and resolve existing bugs.

You can [download an early version of this framework][2] and palette from this site, but I’ll give you a little warning - once you start using objects from a custom IB palette in your code, you need to keep that palette for future reference - if it gets deleted, and you’re still using an object dragged from the custom palette, your nib files will no longer open. I’m also not entirely happy with my cocoa prefix - I think I may move my namespace under my personal company name (boomBalada), but we’ll deal with that when we come to it.

I’ll try to write up a tutorial of how to construct your own custom IB palettes shortly (same bat-time, same bat-channel…).

 [1]: http://virtuedesktops.info/
 [2]: http://static.tonyarnold.com/ColorLabelButton.zip
