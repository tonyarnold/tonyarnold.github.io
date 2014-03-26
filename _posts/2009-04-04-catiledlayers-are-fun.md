---
layout: post
title: CATiledLayers are fun
tags: [Cocoa, Hyperspaces, Programming]
date: 04 April 2009 01:03:00
---

One of the big issues I’m trying to address for [Hyperspaces][1] 1.0 is related to video memory:

Core Animation likes to cache any imagery you insert into a layer onto the user’s graphics card, which is fantastic when you’re running on a machine with more than 256Mb VRAM - things are smooth as silk and you get great fades between changes. Unfortunately, for users running on Macs that don’t have that much VRAM there is a big problem - if the image you load into the layer is too big to fit into VRAM, Core Animation just doesn’t draw it. White backgrounds for the win.

Apple’s answer to this problem is the `CATiledLayer`. Basically, it allows you divide a much larger image into smaller chunks that *can* be cached on older video cards. For [Hyperspaces][1], I’m working on replicating the drawing styles of the standard Mac OS X desktop background - “Fit To Screen”, “Fill Screen”, “Stretch To Fill Screen”, “Center” and “Tile”. Tiled desktops are fine - I’m rendering those using a `CATiledLayer` in the build you’re all using right now (1.0fc4).

What’s interesting though is what happens when I play lazy programmer:

<iframe src="//player.vimeo.com/video/3987685?byline=0&amp;portrait=0" width="720" height="451" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen class="widescreen"></iframe>

Lovely, no? It would be a cool effect with a longer fade, and if I weren’t already getting complaints about how slow [Hyperspaces][1] is to change desktop backgrounds right now. I’m still working on the final code - I’ll post it when it’s done for reference - but the simple answer to this problem is twofold:

*   *Make the tiles as large as you can* - this isn’t too tricky. Apple defaults this to 256px by 256px, but I haven’t done enough research to know what’s reasonable - it’s really going to be based upon your target audience, and whether they have decent graphics cards or not;
*   *Cache the “sliced” image pieces* - the video you see above is the result of me slicing a `CGImageRef` up in real time;

I hope you enjoy the (unintended) effect!

 [1]: http://thecocoabots.com/hyperspaces/