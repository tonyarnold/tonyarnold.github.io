---
layout: post
date: 2013-05-24 17:04
title: "Half Arsed Class: NSRulerView"
tags:  HalfArsedClass, Objective-C, NSRulerView, AppKit
---

*This is a little thing I think I'll start doing to relieve frustration after working with awfully designed or just plain buggy classes. Half Arsed Class will pick out classes that have pissed me off from AppKit, Foundation and UIKit. Hopefully I'll also be able to retract these on a semi-regular basis.*

Today's Half Arsed Class is brought to you by the `NSRulerView` class, which allows you to set a completely custom measurement unit setup so that you can draw rulers against your `NSScrollView` instances.

Sadly, **[there's no way to actually get those measurement units back][1]**. So, if you want to customise how the ticks on your ruler are drawn you're completely out of luck. [You'll have to do all of the calculations, all of the math, and all of the drawing yourself][2].

The default `NSRulerView` also updates as required to reflect the magnification level of the scroll view it's tied to. Via a private instance variable. With no other piece of the puzzle exposed.

*\*mouth fart noise\**

It gets better! [The documentation makes reference to][3]:
> "If you want to do custom hash-marks and labels you should first look at doing it with a delegate.  You can do whatever kind of custom hash-marks you want through delegation as long as the hash-marks and labels are evenly spaced."

However, there are no delegate methods that expose anything to do with customising the hash marks. Brilliant QA work there, guys!

So, if you find yourself thinking "NSRulerView looks like what I need!", think again. It's only useful if you want it in exactly the form you find it.

[Radar filed][4]: I need a drink.

 [1]: http://www.cocoabuilder.com/archive/cocoa/175535-nsrulerview-subclass-and-drawhashmarksandlabelsinrect-nsrect-rect.html
 [2]: http://lists.apple.com/archives/cocoa-dev/2011/Aug/msg00471.html
 [3]: http://developer.apple.com/library/mac/DOCUMENTATION/Cocoa/Reference/ApplicationKit/Classes/NSRulerView_Class/Reference/Reference.html#//apple_ref/occ/instm/NSRulerView/drawHashMarksAndLabelsInRect:
 [4]: http://www.openradar.me/13980710
