---
layout: post
title: Logging to your own file using NSLog
tags: [Cocoa, Programming]
date: 17 February 2007 11:30:00
---

{% capture years_ago %}{{ site.time | date: "%Y" | minus:2005 }}{% endcapture %}

> ## Outdated Info
> Hi there! So it's the future now ({{site.time | date: "%Y"}} to be precise) and the recommendations in this post aren't valid anymore.
> I'd recommend you have a look at [CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack) instead of using the code here in anything you're working on.

Have you ever found yourself needing to have your application record quite a bit of data? Think pushing it to the user’s console is messy? (it is!) Here’s your answer. In the `main.m` of your cocoa application, simply add the following imports:

#### Source

```objective-c
#import <stdio.h.
#import <sys/param.h>
```

Then make your “main” method look like this:

```objective-c
int main(int argc, char *argv[])
{
  id pool = [NSAutoreleasePool new];

  NSString *applicationName = [NSString stringWithFormat: @"Library/Logs/%@.log", [[NSBundle mainBundle] objectForInfoDictionaryKey: @"CFBundleName"]];
  NSString *logPath = [NSHomeDirectory() stringByAppendingPathComponent: applicationName];
  freopen([logPath fileSystemRepresentation], "a", stderr);

  [pool release];

  return NSApplicationMain(argc,  (const char **) argv);
}
```

Now, all of your logging messages will be pushed to a log file with the same name as your application under `~/Library/Logs/`.
