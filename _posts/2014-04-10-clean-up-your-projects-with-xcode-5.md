---
layout: post
title: Clean up your projects with Xcode 5
date: 10 April 2014 22:00:00
tags: [Cocoa, Xcode, Tips]
---

Xcode 5 introduced a host of new features, fixes and performance enhancements but it also makes it possible to simplify your Xcode project and discard some maintenance tasks.

## Link Frameworks Automatically

Every Xcode project you've worked with is likely to have a "Frameworks" group at the root of the project. If you're on OS X it might contain things like *Cocoa.framework*, *Foundation.framework* and *CoreData.framework*, on iOS it holds *UIKit.framework* and friends. One of the improvements that came with Xcode 5 was [LLVM Modules](http://clang.llvm.org/docs/Modules.html). One of the improvements that modules brings is the ability to automatically link any system frameworks that you `#import`. This is **awesome**, and it's one less thing you now have to look after.

As long as you're only keeping system frameworks in that group, you can delete it. **Yes, delete the entire "Frameworks" group**. Just ensure that you've enabled "Link Frameworks Automatically" in your Xcode project's settings.

<img src="http://static.tonyarnold.com/xcode-project-settings-lfa.png" alt="Xcode project settings showing 'Link Frameworks Automatically' setting" class="widescreen" />

## Tidy your schemes

When you open up your project's schemes menu, do you see a bunch of schemes from third party projects in there? 

<img src="http://static.tonyarnold.com/xcode-schemes-menu-super-cluttered.png" alt="Xcode schemes menu showing many schemes" class="center" width="265" height="282" />

To clean them up, go to *Product &#8594; Scheme &#8594; Manage Schemes&hellip;* and uncheck *Show* for any that you don't want to see. 

<img src="http://static.tonyarnold.com/xcode-schemes-menu-deps-removed.png" alt="Xcode schemes menu showing just the important schemes" class="center" width="265" height="182" />

> The caveat is that unless you check the "Shared" column, these settings will be reset if your user project settings are ever reset. It's easy enough to reapply.

## Schemes for unit tests are unnecessary

Older projects often show schemes for any unit test bundles you have in your project — you don't actually need to show them at all!

> it was necessary under Xcode 4 to have separate schemes for your test targets so that <abbr title="Continuous Integration">CI</abbr> servers could find and run them (`xcodebuild` didn't support the "test" action until Xcode 5). 

As long as your test targets specify their *Target Dependencies* properly, you can just go to *Product &#8594; Scheme &#8594; Manage Schemes&hellip;* and delete any test schemes that are listed.

<img src="http://static.tonyarnold.com/xcode-schemes-menu-clean.png" alt="Xcode schemes menu looking super sharp" class="center" width="248" height="142" />

Wow, what an improvement. And no loss of functionality!

## Sort your classes

This is a simple one, but manually ordering your classes and groups is a one way to waste a lot of time. Why not just right click on a group/project in the Xcode navigator and select *Sort Files By Name*?

<img src="http://static.tonyarnold.com/xcode-context-menu-sort-files-by-name.png" alt="Xcode context menu showing 'Sort Files By Name' highlighted" class="center" width="283" height="411" />

## Simple is good

Hopefully these tips have helped you clean up your Xcode project a little. Hopefully you've removed a few things you don't really need to see from your line of sight, freeing up a little bit of brain power for something else!