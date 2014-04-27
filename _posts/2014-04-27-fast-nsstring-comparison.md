---
layout: post
title: Fast NSString Comparisons
date: 27 April 2014 21:51:00
tags: [Cocoa, Programming, Performance]
---

Earlier tonight, I came across a snippet of Objective-C code where the author had used `-compare:` instead of `-isEqualToString:` in every instance. My general rule is to always use the highest-level, most readable API unless there is a critical performance
issue when doing so, so I was intrigued (although I was pretty sure why this was being done):

Here's the simple test I ran:

{% highlight obj-c %}
NSString *someString = @"LANA!";
NSString *otherString = @"LAAANAA!";

NSTimeInterval start = [NSDate timeIntervalSinceReferenceDate];

BOOL boop = [someString isEqualToString:otherString];
NSLog(@"%f", [NSDate timeIntervalSinceReferenceDate] - start);

start = [NSDate timeIntervalSinceReferenceDate];
BOOL phrasing = [someString compare:otherString] == NSOrderedSame;
NSLog(@"%f", [NSDate timeIntervalSinceReferenceDate] - start);
{% endhighlight %}

## Results

- `-isEqualToString:` == 0.000014
- `-compare:` == 0.000007

Turns out that `-compare:` is roughly twice as fast as `-isEqualToString:`.

Personally, I'm going to stick to `-isEqualToString:` unless performance is absolutely critical — I find it much more readable.
