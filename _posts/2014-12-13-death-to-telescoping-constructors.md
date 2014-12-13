---
layout: post
title: "Swift: Death to Telescoping Constructors"
date: 13 December 2014 15:00:00
tags: [Swift, Programming, Learning]
---

One of the many things about Swift that has made me happy is the introduction of default parameter values on methods. In Objective-C, it's pretty common to see APIs that looks a lot like the following code (taken from MagicalRecord):

{% highlight objective-c %}

// NSManagedObjectContext+MagicalFinders.h

+ (instancetype)findFirstInContext:(NSManagedObjectContext *)context;

+ (instancetype)findFirstWithPredicate:(NSPredicate *)searchTerm 
                             inContext:(NSManagedObjectContext *)context;
                             
+ (instancetype)findFirstWithPredicate:(NSPredicate *)searchterm 
                              sortedBy:(NSString *)property 
                             ascending:(BOOL)ascending 
                             inContext:(NSManagedObjectContext *)context;


// NSManagedObjectContext+MagicalFinders.m

+ (instancetype)findFirstInContext:(NSManagedObjectContext *)context
{
  return [self findFirstWithPredicate:nil 
                             sortedBy:nil 
                            inContext:context];
}

+ (instancetype)findFirstWithPredicate:(NSPredicate *)searchTerm 
                             inContext:(NSManagedObjectContext *)context
{
  return [self findFirstWithPredicate:searchTerm 
                             sortedBy:nil 
                            ascending:YES 
                            inContext:context];
}

+ (instancetype)findFirstWithPredicate:(NSPredicate *)searchterm 
                              sortedBy:(NSString *)sortedBy 
                             ascending:(BOOL)ascending 
                             inContext:(NSManagedObjectContext *)context
{
  // Actual implementation of method
}

{% endhighlight %}

This pattern is often referred to as the "telescopic pattern", or "telescoping methods". Basically, you implement a number of methods that each call the next, more specific method in the chain, providing default values at each stage as they become necessary. Users of the API can choose to use any of the methods, allowing for more succinct code, but only requiring a single "real" method implementation.

In Swift, this functionality is built into the language (hooray!). As an example, given the following method in Swift:

{% highlight swift %}
func findFirstWithPredicate(predicate:NSPredicate? = nil,
                            sortedBy:String? = nil,
                            ascending:Bool = true,
                            inContext context:NSManagedObjectContext) -> [NSManagedObject] {
  // Actual implementation of method
}
{% endhighlight %}

Users of this Swift API can choose _not to include any parameters that have default values_, ie:

{% highlight swift %}
let results = findFirstWithPredicate(inContext:myContext);

// OR 

let otherResults = findFirstWithPredicate(sortedBy:"someProperty", 
                                          inContext:myContext);

// OR

let moreResults = findFirstWithPredicate(sortedBy:"someProperty", 
                                         ascending:false, 
                                         inContext:myContext);

// You get the gist of it!
{% endhighlight %}

This allows for much more succinct methods calls, without the mountain of boilerplate we would have had to write in Objective-C!
