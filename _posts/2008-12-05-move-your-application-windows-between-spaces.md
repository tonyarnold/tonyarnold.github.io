---
layout: post
title: Move your application windows between spaces
tags: [Cocoa, Programming]
date: 05 December 2008 22:57:00
---

I puzzled for a few hours over this the other night - it’s something that used to work in VirtueDesktops, and for some reason I just assumed it no longer functioned under Mac OS X 10.5. Aside from an embarrassing bout of forgetting to get the window number properly, this turned out to be remarkably simple.

## Prerequisites

You’ll need a copy of the [CGSPrivate header][1] in your project.

## How to

Simply use the following code, where `ibo_window` is an Interface Builder outlet to an NSWindow in your XIB file:

{% highlight obj-c %}
CGSWindowID windowId = (CGSWindowID)[ibo_window windowNumber];

// The following integer represents the space you want to move the 
// window to - the array is not zero-based - Space 1 == 1, Space 2 == 2, 
// etc
NSInteger spaceToMoveTo = 2;

// Window count can be more than one, but for this example we're 
// using a single window
NSInteger windowCount = 1;

// Now for the magical call:
CGSMoveWorkspaceWindowList(_CGSDefaultConnection(), 
                           &amp;windowId, 
                           windowCount, 
                           spaceToMoveTo);
  
// If you want to check which space a window is on, simple use the 
// following code:
NSInteger windowId = -1;  

CGSGetWindowWorkspace(_CGSDefaultConnection(), 
                      windowId, 
                      &amp;workspaceID);

NSLog(@"Your window is now on space %i", windowId);
{% endhighlight %}

Easy, huh? I’m pretty sure this won’t work across processes (that’s why all the old desktop managers insert code into the running Dock application - it’s one of the only applications that has permission to muck about with other application’s windows). You should also probably try to intercept any errors thrown by the `CGS*` methods, but I’ll leave that as an exercise to you, gentle reader.

 [1]: http://code.google.com/p/undocumented-goodness/source/browse/trunk/CoreGraphics/CGSPrivate.h