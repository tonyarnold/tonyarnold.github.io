---
layout: post
title: Integrated documentation for Xcode projects
tags: [Cocoa, Programming]
date: 28 March 2008 15:05:00
---

I’ve been thinking for the past week or so about how I can contribute something back to the mac development community - a lot of good people spend a lot of time helping me out with my issues as they come up, and I believe improving our toolchain is probably the best way for me to contribute. Documentation, to be specific.

If we take the time to properly document and comment our source code, we’re unlikely to want to have to re-document that into a human readable format such as HTML or PDF, right? I’ve previously used tools such as [HeaderDoc][1] and [NaturalDocs][2] depending on the language and framework I’m coding in to achieve this end – with wildly varying results. HeaderDoc’s default output is quite ugly, and has some glaring omissions in terms of it’s parsing of some of the newer documentation tags.

So I’m thinking about starting up a [Google Code][3] project around this, and I’m just trying to get a feel for what people think about this idea, what they would use, and how they would see this working. So far I’ve solicited a little feedback and the following are things I know I’d like to see:

*   **Xcode build integration**: the generation of this documentation should work as part of the Xcode build process. No messing around with external tools; 
*   **Comment formats should use what’s already out there**: Lots of our code is already documented using HeaderDoc’s comment format - we should try to expand upon that if we need to - not replace it (but I’m open to suggestion here);
*   **The generated output should look good**. No arguments there.

Comments ahoy, my peers!

 [1]: http://developer.apple.com/opensource/tools/headerdoc.html
 [2]: http://www.naturaldocs.org/
 [3]: http://code.google.com/