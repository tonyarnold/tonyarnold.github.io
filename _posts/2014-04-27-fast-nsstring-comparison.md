---
layout: post
title: Fast NSString Comparisons
date: 27 April 2014 21:51:00
tags: [Cocoa, Programming, Performance]
---

> About 35 seconds after I posted this article, [Lawrence Lomax pointed out](https://twitter.com/insertjokehere/status/460387480211300352) that Mark Dalrymple had [already published exhaustive details about NSString comparisons on the Big Nerd Ranch blog](http://blog.bignerdranch.com/334-isequal-vs-isequaltostring/). Go read that and stop wasting your time over here!

Earlier tonight, I came across a snippet of Objective-C code where the author had used `-compare:` instead of `-isEqualToString:` in every instance. My general rule is to always use the highest-level, most readable API unless there is a critical performance
issue when doing so, so I was intrigued (although I was pretty sure why this was being done):

Here's the simple test I ran:

{% highlight obj-c %}
NSString *someString = @"LANA!";
NSString *otherString = @"LAAANAA!";
NSString *sameString = @"LANA!";

NSTimeInterval start = [NSDate timeIntervalSinceReferenceDate];

BOOL boop = [someString isEqualToString:otherString];
NSLog(@"%f", [NSDate timeIntervalSinceReferenceDate] - start);

start = [NSDate timeIntervalSinceReferenceDate];
BOOL bleep = [someString compare:otherString] == NSOrderedSame;
NSLog(@"%f", [NSDate timeIntervalSinceReferenceDate] - start);


start = [NSDate timeIntervalSinceReferenceDate];
BOOL boopSame = [someString isEqualToString:sameString];
NSLog(@"%f", [NSDate timeIntervalSinceReferenceDate] - start);

start = [NSDate timeIntervalSinceReferenceDate];
BOOL bleepSame = [someString compare:sameString] == NSOrderedSame;
NSLog(@"%f", [NSDate timeIntervalSinceReferenceDate] - start);
{% endhighlight %}

## Results

| Method            | Result                | Time Logged (seconds) |
|:------------------|:----------------------|:----------------------|
|`-isEqualToString:`| Strings did not match | 0.000014              |
|`-compare:`        | Strings did not match | 0.000007              |
|`-isEqualToString:`| Strings matched       | 0.000001              |
|`-compare:`        | Strings matched       | 0.000002              |

Turns out that `-compare:` is roughly twice as fast as `-isEqualToString:` when the strings don't match and the inverse is true when the strings match — although with the matching strings the difference is very nearly negligible.

Personally, I'll probably stick to `-isEqualToString:` unless performance is absolutely critical — I find it much more readable, and that's almost always more important than saving 0.000007 seconds.
