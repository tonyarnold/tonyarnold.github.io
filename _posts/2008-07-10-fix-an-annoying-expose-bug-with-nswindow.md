---
layout: post
title: Fixing an annoying Exposé bug in NSWindow
tags: [Cocoa, Programming]
date: 10 August 2008 22:20:00
---

![An image of my desktop with the Exposé bug visible on two foreground iChat windows][1]

You’ve seen it before - Exposé’s F-10 mode stops working for no apparent reason. F-9 is still good to go, but F-10 just looks busted.

## Why?

Your application has set one of it’s `NSWindow` instances to the desktop level or lower (`kCGDesktopIconWindowLevel` or `kCGDesktopWindowLevelKey` are where it all seems to start).

## Can I fix it?

Yes - fixing this problem is simple - either stop using windows at or below the desktop icon level, or add the following code to a window category or subclass in your project and execute the “`clearExposeTags`” method upon an active instance of your troublesome `NSWindow`. If you’re using `CGSPrivate.h`, you can just include the method without all the `typedefs` and `extern`s.

{% highlight objc  %}
typedef int CGSConnection;

typedef int CGSWindow;

typedef enum {
    CGSTagNone          = 0,        // No tags
    CGSTagExposeFade    = 0x0002,    // Fade out when Expose activates.
    CGSTagNoShadow      = 0x0008,    // No window shadow.
    CGSTagTransparent   = 0x0200,   // Transparent to mouse clicks.
    CGSTagSticky        = 0x0800,    // Appears on all workspaces.
} CGSWindowTag;

extern CGSConnection _CGSDefaultConnection(void);

extern CGError CGSClearWindowTags(
	const CGSConnection cid, 
	const CGSWindow wid, 
	CGSWindowTag *tags, 
	int thirtyTwo);

- (OSStatus)clearExposeTags
{
    CGSConnection cid;
    CGSWindow wid;
    CGSWindowTag tags[2];
    
    wid = [self windowNumber];
    cid = _CGSDefaultConnection();
    tags[0] = 0x02;
    tags[1] = 0;
	
    return CGSClearWindowTags(cid, wid, tags, 32);
}
{% endhighlight %}

 [1]: http://static.tonyarnold.com/missing_shadows-1306152494.jpg "Missing shadows on windows in Exposé"
 [2]: http://plasq.com/
 [3]: http://skitch.com
