---
layout: post
title: ReactiveLessons
date: 2013-05-13 08:55
tags: [Cocoa, ReactiveCocoa, Objective-C]
---

In my experience, there are three simple ways to think about using [ReactiveCocoa][RAC]:

* As a lovely, simple replacement API for Key-Value Observation;
* As a way to introduce Functional Reactive Programming (FRP) into Cocoa apps;
* A hybrid of the two.

## Key-Value Observation Done Right

Here's the current state of using Key-Value Observation to observe and respond to changes to a string property on my fictional class:

{% highlight objective-c %}
// In your viewDidLoad/awakeFromNib/init
[self addObserver:self
       forKeyPath:@"someString"
          options:NSKeyValueObservingOptionNew
          context:&someStringChangeContext];

// In dealloc
[self removeObserver:self
          forKeyPath:@"someString"
             context:&someStringChangeContext];

// Elsewhere in your class
- (void)observeValueForKeyPath:(NSString *)keyPath
                      ofObject:(id)object
                        change:(NSDictionary *)change
                       context:(void *)context
{
    if (context == &someStringChangeContext) {
        if ([keyPath isEqualToString:@"someString"]) {
            // Do a bunch of stuff here
        }
    }
}
{% endhighlight %}

Here's the same thing using ReactiveCocoa:

{% highlight objective-c %}
[RACObserve(self, someString) distinctUntilChanged] subscribeNext:^(NSString *string) {
    // Do a bunch of things here, just like you would with KVO
}];
{% endhighlight %}

There's no need to tear down the observer when you're done, and [ReactiveCocoa][RAC] even takes care of weeding out non distinct changes for you! If you're only interested in using ReactiveCocoa as a simple replacement for KVO, there you go. "Bam" said the lady.

## 'Bringing It' Functional Reactive Style

The real drive behind the GitHub team building ReactiveCocoa is something called "[Functional Reactive Programming](http://blog.maybeapps.com/post/42894317939/input-and-output?3ed07280)" (or FRP). I'm the first to admit that I don't always understand the most elegant way to approach problems in Cocoa apps using FRP, but the basic gist is that you're removing unnecessary state from your code.

In the KVO example above, we're dealing with a string property on a fictional class instance, the actual real-world use of this would not be so abstract. It's likely that we're taking a string value from some data source and displaying it in a text field. So here's that:

{% highlight objective-c %}
RACSignal *nameSignal = [RACObserve(self, someManagedObject.name) distinctUntilChanged];

RAC(self, someTextField.text) = [nameSignal deliverOn:[RACScheduler mainThreadScheduler]];
{% endhighlight %}

Still with me? Every time the `self.someManagedObject.name` attribute changes, that change will automatically propagate to the text field. Conceptually, it's quite a lot like Cocoa Bindings, but unlike bindings it's available for use on iOS.

But that's still not the real advantage of ReactiveCocoa. Consider this, you have an `NSDate` property on one of your objects that you'd like to display in a text field. ReactiveCocoa can help you do that, while providing the same binding-style advantages as above:

{% highlight objective-c %}
RACSignal *dateSignal = [RACObserve(self, someManagedObject.startDate) distinctUntilChanged];

RAC(self, someTextFieldForShowingTheDate.text) = [[dateSignal map:^NSString *(NSDate *date) {
    return [NSDateFormatter localizedStringFromDate:date
                                          dateStyle:NSDateFormatterShortStyle
                                          timeStyle:NSDateFormatterShortStyle];
}] deliverOn:[RACScheduler mainThreadScheduler];
{% endhighlight %}

Now any time the date changes on the managed object, the text field will automatically update as well, converting from `NSDate` to `NSString` as it goes. Nifty, hey?

## Danger! High Voltage Reactions

So ReactiveCocoa, yay! More succinct code, yay! "Should I be using this right now?" I hear you ask?

In the course of adopting ReactiveCocoa for use in my own projects, I've discovered some not awesome things:

* Thinking about things in an FRP way currently takes longer for complex situations. At least for now, I'm finding I spend a lot less time on the simple interactions between my data and the UI, but a lot longer on complex problems. There's a lot of abstract thinking and explanations in FRP;
* It's really easy to end up with hundreds of lines of subscriptions and maps for more complex UIs — I call this "ReactiveSpaghetti". I don't think this problem is unique to ReactiveCocoa, but it's easier to see it in action when your `- (void)viewDidLoad` method turns into a RACParty;
* A lot of Xcode and LLDB's nice debug handling doesn't work well with ReactiveCocoa. You will be dumped into an untraceable stream of RACSignals and blocks at some point. Don't even get me started on crash reports that originate from within ReactiveCocoa! There are logging methods built into ReactiveCocoa, but they're not going to do you any good with a user-uploaded crash log;

So ReactiveCocoa is not all peaches and cream, but to date I've also noticed no performance issues and I feel like I'm expressing myself more clearly through RAC-enabled code than I was beforehand.

**After my experiences, I could quite happily just stick to using `subscribeNext:` and `map:` methods in a very simple, KVO-esque manner.**


 [RAC]: https://github.com/ReactiveCocoa/ReactiveCocoa/
