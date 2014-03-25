---
layout: post
date: 2013-10-13  
title: CoreData.next
---

I've been using Core Data since it was introduced in Mac OS X 10.4 "Tiger", and it's my first choice anytime I need to save structured data in my apps.

The problem is, **everyone uses Core Data because there's nothing better**. It's the best way to persist structured data on iOS and OS X, but it's not actually much fun to implement and has many warts. **To be utilised properly, Core Data requires a level of experience and knowledge that's simply not reasonable to expect from people starting out with Cocoa development** — although it does it's best to convince you otherwise with the visual Core Data Modeller in Xcode.

Something as base as saving data should be much, much easier.

Before I really get stuck in, let me be clear: there are probably legitimate reasons why Core Data does all of the things I highlight. I'm not insinuating for a minute that any of my suggestions are even technically possible — this is what I would investigate for a major revision to Core Data (were it my call, which it is not).

## Setting up is too much work

Creating a usable Core Data stack for your application by hand requires far too much boilerplate. Apple should be providing a very basic `[NSCoreDataStack newStackWithOptions:…]` or something similar that gets your app up and running with the best possible set of defaults.

Libraries like MagicalRecord provide this now, but it seems odd that the Core Data framework does little to aid setting up the stack in a recommended manner.

## It's workarounds all the way down and then you hit NSMangedObject

Yes, I meant to spell it that way.

In the last couple of years, Apple have made attempts to simplify and extend some parts of Core Data, including the addition of parent contexts, and methods to help run your code on the correct thread for a specific `NSManagedObjectContext` (i.e. `-(void)performBlock:` and `-(void)performBlockAndWait:`).

The problem is, **these additions are essentially workarounds for problems that shouldn't really be the concern of the developer** using the API.

The additions I cited above all stem from `NSManagedObjectContext` and `NSManagedObject` instances not being thread safe. I'd rather see Apple create new, non-backwards compatible API to solve this than continue to patch underlying design issues with new API. I get this one is not trivial. Threading never is.

## Except the exceptions

If you've used Core Data, chances are you've seen it do it's best impression of a monkey in a cage. It flings internal NSExceptions around like a monkey with poop. Debugging a Core Data app with lldb intercepting all exceptions is an exercise in frustration and sifting through "what's yours" and "what's mine".

I'd like to see all exceptions thrown by the framework properly caught and dealt with before the developer ever sees them in Xcode.

## Easier handling of binary data

One of the common things new users of Core Data try to do is store images and other data in their SQLite persistent store. It's entirely possible to do so, and the addition of external binary representations for Binary attributes helps improve performance when doing so.

The issue is, accessing that data can have significant memory implications as you can't really take advantage of any of the great optimisations Apple has made to image/file loading without first dumping the data of the attribute into a temporary file outside of your store.

Want to use any of the audio visual frameworks to access media that you've stored in your persistent store? Forget it. They all need a URL or file path.

Allowing direct access to binary data attributes external file URLs (and allowing access to read that file via the URL) would greatly simplify this scenario, and I'd imagine it would reduce disk I/O.

## NSFetchedResultsController on both platforms

I use `NSFetchedResultsController` in almost all of my iOS apps. I set it up and forget about it, and it takes care of marshalling any changes to my datasources. `NSArrayController` is the prototype that we have on OS X, and it's just not setup to handle things like animating UI changes in table views and the like.

A simple, fast way to automatically query and update a datasource and handle discrete changes on both platforms would be a huge time saver. Making it capable of doing it's work nicely on a background thread would be a big win, too.

## Performance and simplicity

Any improvements to performance in any API are always a good thing, but Core Data has some specific areas that could use attention. Anything involving batch operations could use a bit of love (as outlined by Brent in his [series of posts on Core Data in Vesper](http://inessential.com/2013/10/05/vesper_sync_diary_2_core_data)).

Honestly though, I think Core Data.next needs to be simpler to implement and interact with:

* There's a lot in Core Data right now that just seems to be there for the sake of working around the lack of thread safety
* I know it's not everyone's cup of tea, but simpler queries and searches would be ace
* Roll the work Wolf has done on [mogenerator](http://rentzsch.github.io/mogenerator/) into Xcode — the attribute structs and entityName methods should be there for all `NSManagedObject` subclasses

This is all pie in the sky, but it's nice to dream right?

And maybe to implement. Maybe.

Hit me up on [Twitter](http://twitter.com/tonyarnold/) or [App.net](http://alpha.app.net/tonyarnold/) with your thoughts, or even better — write a post in response.

## Responses

* [Robbie Hanson has answered my post](http://deusty.blogspot.com.au/2014/01/response-coredatanext.html) putting forward [YapDatabase](https://github.com/yaptv/YapDatabase) as a viable replacement (and improvement) for Core Data. I'm keen to have a look at it for my next project.
