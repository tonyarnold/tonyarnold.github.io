---
layout: post
title: "Convenience #DEFINEs"
tags: [Cocoa, Programming]
date: 05 July 2008 13:00:00
---

> ***Update:** Lazy programmer, indeed! After doing some research myself this afternoon (at the prompting of Karsten), I’d recommend not using anything but the `ZNCGAutoRelease()` method below - the others aren’t dangerous, but they’re really not necessary and just obscure your ability to properly debug your code. As for using macros, well, I guess that’s a matter of personal preference - what I’ve seen so far is that it does make debugging harder - you’re probably better off implementing proper methods for repeatable tasks. But it works if you want to use it.*

When I first started working on VirtueDesktops (all those years ago), I was still new to Objective-C and very new to the concept of (mostly) manual memory management. Thankfully Thomas (the previous developer) had the foresight to do what all good, lazy programmers should do and write himself a few small convenience methods into his codebase.

They’ve had a couple of minor additions and changes since then, but line-for-line, they’ve stood the test of time and I find them an invaluable way to reduce some of the fuss involved in manually managing your object assignments, copies and releases.

{% highlight objc %}
#define ZNCGAutoRelease(x) (__typeof(x))[NSMakeCollectable(x) autorelease]

#define ZNAssign(aTarget, aSource)  \
if (aTarget != nil) {               \
    [aTarget autorelease];          \
}                                   \
aTarget = [aSource retain];

#define ZNAssignCopy(aTarget, aSource)  \
if (aTarget != nil) {                   \
    [aTarget autorelease];              \
}                                       \
aTarget = [aSource copy];

#define ZNRelease(aTarget)          \
if (aTarget != nil) {               \
    id oldObject = aTarget;     \
    aTarget = nil;                  \
    [oldObject release];            \
}
{% endhighlight %}

I use these **everywhere** in my code, but just the other day I discovered the absolutely incredibly wonderful [CLANG Static Analysis][1] tools (more on this shortly!), and based on some feedback it gave around these calls (nothing bad!) it made me wonder - should I be `#DEFINE`ing convenience methods? Is this best practice? Should I go back to doing this all by hand?

I’m hoping some of my CocoaPeers™ will be able to provide me with some advice here, but if you think the code’s good for your needs - go for your life and use it.

Oh, and happy 4th of July to our friends in the states. We’re waiting for you here on the 5th :)

 [1]: http://clang.llvm.org/StaticAnalysis.html