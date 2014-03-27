---
layout: post
title: "Detecting when the active Space changes"
tags:
  - Cocoa
  - Programming
date: 11 November 2007 00:00:00
---

OK, so there's been a discussion about this on the cocoa-dev list of late, and no-one answered the question - I figure I'll jump into the fray given that this is exactly what I've been working on with Hyperspaces.

There are two things you have to understand up front:

**There is a notification “com.apple.switchSpaces” posted when a user chooses to switch spaces via the menu extra**. This notification can also be (ab)used to switch spaces using your app as well - however…

**There is no other notification that your active space has changed**, and it is only posted by the menu extra. **You need to check for changes from the CoreGraphicsServer** - the easiest way to do that is as follows. It's up to you to write the code that uses this, but attaching it to a simple NSTimer would probably work just fine.

{% highlight obj-c %}
-(NSNumber *)CGSSpaceNumber
{
  int spaceNumber = -1;
  CGSGetWorkspace(_CGSDefaultConnection(), &spaceNumber);
  return [NSNumber numberWithInt: (spaceNumber - 1)];
}
{% endhighlight %}

I use this method in [Hyperspaces][hsurl], and it works just fine for my purposes (with the requisite delay associated with my application having to scan for changes). Apple's Eric Schlegel [explains the reasoning behind why there is no notification on the cocoa-dev list][cocoa-dev post]. Long story short, it sounds like Apple's not quite done developing Spaces yet, and they don't want people relying on APIs that aren't finalised.

 [hsurl]: http://thecocoabots.com/hyperspaces/
 [cocoa-dev post]: http://www.cocoabuilder.com/archive/message/cocoa/2007/11/11/192797
