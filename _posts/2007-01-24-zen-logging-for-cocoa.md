---
layout: post
title: Zen Logging for Cocoa
tags: [Cocoa, Programming]
date: 24 January 2007 23:00:00
---

{% capture years_ago %}{{ site.time | date: "%Y" | minus:2005 }}{% endcapture %}

> ## Outdated Info
> Hi there! So it's the future now ({{site.time | date: "%Y"}} to be precise) and the recommendations in this post aren't valid anymore. I'd recommend you have a look at [CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack) instead of using the code here in anything you're working on.

How many times have you found yourself coding some *“sick cocoa code… gosh”* (excuse the Napoleon Dynamite reference there), and thought - *“Gee whiz Myself, `NSLog` sure is sorta limp in the actual informative-ness stakes, ain’t it?”*

Me? All the time. So I did a bit of [hunting about][1] and devised the following logging class based upon comments by Scott Morrison:

#### Source

{% highlight obj-c %}

#import <Cocoa/Cocoa.h>

@interface ZNLog : NSObject {}

+(void)file:(char*)sourceFile function:(char*)functionName lineNumber:(int)lineNumber format:(NSString*)format, ...;

#define ZNLog(s,...) [ZNLog file:__FILE__ function: (char *)__FUNCTION__ lineNumber:__LINE__ format:(s),##__VA_ARGS__]

@end

@implementation ZNLog

+ (void)file:(char*)sourceFile function:(char*)functionName lineNumber:(int)lineNumber format:(NSString*)format, ...
{
  NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
  va_list ap;
  NSString *print, *file, *function;
  va_start(ap,format);
  file = [[NSString alloc] initWithBytes: sourceFile length: strlen(sourceFile) encoding: NSUTF8StringEncoding];

  function = [NSString stringWithCString: functionName];
  print = [[NSString alloc] initWithFormat: format arguments: ap];
  va_end(ap);
  NSLog(@"%@:%d %@; %@", [file lastPathComponent], lineNumber, function, print);
  [print release];
  [file release];
  [pool release];
}

@end
{% endhighlight %}

#### License

It’s all licensed under [Creative Commons Attribution 2.5][3] license, so just be sure to include a short attribution back to me in your header/notes/readme.

 [1]: http://outerlevel.com/blog/2006/12/01/code-review/
 [3]: http://creativecommons.org/licenses/by/2.5/
