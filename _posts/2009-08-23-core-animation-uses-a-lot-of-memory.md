---
layout: post
title: Core Animation uses a lot of memory
tags: [Cocoa, Hyperspaces, Programming]
date: 23 August 2009 22:22:00
---
Here’s something Apple should probably put on the box when they sell Core Animation to new developers: It uses a *lot* of RAM. Before you dive in with both feet, you need to ask whether the features you get from Core Animation will really be worth the overhead.

In [Hyperspaces][1], if you’re running on a single monitor set-up, you’ll generally see RAM usage around the 60-100Mb mark (RSIZE). Two screens, you’re going straight beyond the 100Mb mark. I assume it grows exponentially from there, but I’ve no machines on hand that will drive more than 2 screens (*Update:* I assume wrong - the caching is pretty good for CGImageRefs and their ilk. It won’t grow exponentially).

On a single monitor set-up, there are two layer-backed views - one screen-size view that sits behind your desktop icons, and one smaller view that contains the switcher. If I run up Hyperspaces without either of my layer-backed views enabled, the application uses 13Mb RAM - so the core (for what it does) is quite compact. If I re-enable the layer-backed switcher window, memory usage instantly jumps to 56Mb - the switcher is usually about 500 - 600px wide, and about 100px high (with 3 spaces enabled).

I have spent *months* trying to bring this number down by any means possible. So far, I’ve tried:

1.  Cropping and chopping my [CGImageRef][2] objects down to only exactly what’s needed for display;
2.  Aggressively caching and uncaching [CGImageRef][2] objects (thanks go out to [Sean O’Brien][3] for helping me with that);
3.  Storing only the [CGImageSourceRef][4] for each of my images and explicitly telling those sources not to cache their [CGImageRefs][2];
4.  Saving those cropped and chopped [CGImageRef][2] objects out to cached JPEG2000 files and then reading those files back into cached [NSData][5] objects to be decoded when needed;

There are probably other things I’ve tried that have worked to varying degrees, but those items above are the ones that made a difference. They don’t solve the problem.

If you’re writing a background application that you expect your users to have open all the time, you (unfortunately) will need to think very carefully about whether you should use Core Animation in your application. I’ve had feedback from users of [Hyperspaces][1] that they would prefer to leave the animation in - while I pitch [Hyperspaces][1] as a tool that provides context to Apple’s Spaces, I’m pretty sure a lot of the users are more into the eye candy and the softly fading desktop images :)

I’ve certainly asked for advice about this issue in a few different places, as well as done my research - and I’d be very happy to be proven wrong (please?!).

 [1]: http://hyperspacesapp.com/
 [2]: http://developer.apple.com/documentation/graphicsimaging/reference/CGImage/Reference/reference.html
 [3]: http://seanpatrickobrien.com/
 [4]: http://developer.apple.com/documentation/graphicsimaging/Reference/CGImageSource/index.html
 [5]: http://developer.apple.com/documentation/Cocoa/Reference/Foundation/Classes/NSData_Class/index.html
