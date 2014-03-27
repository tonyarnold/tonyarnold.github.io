---
layout: post
title: Xgl and the future of Virtue
date: 08 February 2006 19:00:00
tags: [VirtueDesktops]
---

Wow. Holy goddamn crap.

[http://www.novell.com/linux/xglrelease/][1]

Watch the movies. Especially the cube. I’m sorry guys, but it will be a while before I can make a desktop manager that will do that on the mac. As I mentioned in my earlier posts about Virtue, I’m just starting out with mac programming - if people want to see a desktop manager similar to the one Nat and co demoed, I’m going to need guru help. Virtue has basically hit a wall in terms of visuals — we’re limited to what Apple decides to include in the CoreGraphics/Dock code, and even then, they could pull all the transitions at any point. We need a way forward.

Here’s a list of things I’m looking into, but would appreciate advice on from anyone in the know:

* The internals of how Mac OS is presently managing the existence of two user accounts logged in at the same time in relation to NSWorkspace/desktops. You may have noticed that Virtue presently changes desktops and **then** the desktop picture changes, whereas in fast user switching the desktop picture is *part of the transition*. I’m sure I’m missing something small in the entirely undocumented, entirely unsupported calls I’m making (:P), but if anybody else has ever looked at this code, and has any ideas, I’m all ears!
* OpenGL vs. CoreImage. As much as I’d love to use CoreImage as the basis for whatever effect/transition engine this new desktop manager uses, from what I’ve seen CI transitions are slow. Especially for large images. Am I right in assuming that OpenGL is likely to be more efficient? What is being used in Keynote? I would love to have the extensibility of CoreImage though…

Don’t count this as being an announcement of an actual product yet - I **want** to make this happen, but I’m not even sure it’s possible. Chances are that I’ll spend the next 7 months writing something, and 10.5 will include everything we’re looking for (fingers crossed!).

Am I nuts? Wait… don’t answer that…

 [1]: http://www.novell.com/linux/xglrelease/
