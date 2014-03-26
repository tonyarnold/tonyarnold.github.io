---
layout: post
title: "What to do when all you have is symbLOLication"
tags:  [Cocoa, Programming, Xcode]
excerpt: "I've been battling a pesky case of missing symbols when debugging on iOS-based devices lately. It only started when I upgraded to Xcode 4. I was beginning to think I'd be symbolicating by hand until Apple sorted things out — fear not, I've found a workaround!"
---

![alt:Instruments icon;; class:left;; style:margin-top:5px;background-image:none;border-width:0px;background-color:transparent;-webkit-box-shadow:none;-mozilla-box-shadow:none;box-shadow:none](http://static.tonyarnold.com/instruments-1306143920.png)I've been battling a pesky case of missing symbols when debugging on iOS-based devices lately. It only started when I upgraded to Xcode 4. I was beginning to think I'd be symbolicating by hand until Apple sorted things out — fear not, I've found a workaround!

1. First up, profile your app using **Instruments.app** — I use the '**Time Profiler**' instrument, because it's pretty easy to see when things aren't symbolicating properly. If you're (un)lucky, your app will profile just fine, but you'll be left with a bunch of addresses rather than nicely named methods and functions;
2. Stop profiling your app, but don't close the Instruments document;
3. Go to '**File >> Re-Symbolicate Document…**';
4. Find your app's name in the list (search if you have to) and select it;
5. Click the '**Locate**' button, and find the dSYM for your app (as of Xcode 4, it'll be in <code>~/Library/Developer/Xcode/DerivedData/$PRODUCT/Build/Products/Debug-iphoneos/</code>)
6. Once you've done this, click OK and voila symbol names should spring to life!

Any subsequent runs of your app in this Instruments document should properly symbolicate, allowing you to get back to making your app faster and smoother — enjoy!