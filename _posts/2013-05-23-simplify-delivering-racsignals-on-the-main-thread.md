---
layout: post
title: Simplify delivering RACSignals on the main thread
date: 2013-05-23 09:56
source: http://gist.github.com/tonyarnold/5631849
tags:  [Cocoa, ReactiveCocoa, Objective-C]
---

One of the common things you'll do when working with [ReactiveCocoa](http://github.com/ReactiveCocoa/ReactiveCocoa/) is ensure that signals are delivered on the main thread. This is important when sending signals to user interface elements which (in general on OS X and always on iOS) must be delivered on the main thread.

Compare:

{% highlight obj-c %}
RACSignal *zoomSignal = [RACObserve(self, zoom) distinctUntilChanged];
RAC(self, rulerView.tickFrequency) = [[zoomSignal map:^NSNumber *(NSNumber *zoom) {
    return @(4.f * zoom.floatValue);
}] deliverOn:[RACScheduler mainThreadScheduler]];
{% endhighlight %}

To:

{% highlight obj-c %}
RACSignal *zoomSignal = [RACObserve(self, zoom) distinctUntilChanged];
RAC(self, rulerView.tickFrequency) = [[zoomSignal map:^NSNumber *(NSNumber *zoom) {
    return @(4.f * zoom.floatValue);
}] deliverOnMainThread];
{% endhighlight %}

It's not a huge saving, but when you're dealing with complex compositions, I've found it does make a difference to a signal's readability.
