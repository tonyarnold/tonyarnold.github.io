---
layout: post
title: "Private methods in Objective-C using categories"
tags: [Cocoa, Programming, Tutorial]
date: 04 May 2010 01:15:00
---

<img src="http://static.tonyarnold.com/danger_of_pulling_down_with_cage-1306152934.jpg" alt="Photo of a badly translated warning sign in Croatia" class="widescreen" />

Objective-C is an incredibly flexible language, but there are a few things I don't think it handles very elegantly - private methods are one of those things. Private methods are important when designing your classes - keeping the implementation of your methods separate to the interface that users of your class see is good practice, and lets you change the way you implement things in future without making users of your class change their code.

Objective-C has a great feature known as categories. In the [words of Scott Stevenson][1], "a category allows you to add methods to an existing class without subclassing it or needing to know any of the details of how it's implemented". My private methods are implemented using an anonymous category on each class. These are also known as "Class Extensions" and they look like this in my `.m` file:

{% highlight obj-c %}
@implementation MyGreatClass

// Your standard, public methods for the class go here.

#pragma mark - Private Methods

- (void)MyGreatClass_somePrivateMethod
{
  // Implement your private method here.
}

@end
{% endhighlight %}

You'll notice that I preface my private methods with the name of the current class - I do this to avoid method name collisions with subclasses. It's not strictly necessary, but it means I don't have to think as hard when implementing subclasses of my class.

You can do everything you would in a normal class **except** declare new instance variables. I often use my class extensions to redeclare a public `readonly` property as `readwrite` within the confines of the class instance. Another common use in my code are the following two methods:

{% highlight obj-c %}
- (void)MyGreatClass_registerObservers
{
	// …
}

- (void)MyGreatClass_unregisterObservers;
{
	// …
}
{% endhighlight %}

These methods are used to set up and tear down any Key/Value Observers and bindings for the current class. I use these so often that [I've put together an Xcode class template][2] so that they are included in my classes by default.

Please **keep in mind that Objective-C has no true implementation of private methods** - other classes can use these "private" methods if they know the structure of the method in question. With that said, I still believe this is a great way to keep your implementation as clean as possible.

## Update ##

Both Paul and Collin make good points in the comments - you can just declare your private methods inline in your class without using an anonymous category. That will work so long as the declaration occurs before the first use of the method. In my mind, there are two good reasons to use a category:

* **Readability/cleanliness** - I find it a lot easier to group the declarations for my private methods together inside the category block. It's quite readable and means I can just look at the start of the source for each of my classes to see what private methods are defined;
* **It's the same when compiled** - as I understand it, anonymous categories are compiled into the same space as the methods for the class they are defined for. Functionally - once the code is compiled - there shouldn't be any difference between the two ways of defining the methods.

 [1]: http://cocoadevcentral.com/d/learn_objectivec/
 [2]: http://github.com/tonyarnold/CocoaBotsXcodeTemplates/