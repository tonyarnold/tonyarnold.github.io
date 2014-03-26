---
layout: post
title: Releasing a public beta of your application
tags: [Cocoa, Programming]
date: 02 March 2008 00:57:00
---

*Take what I’ve posted here with a grain of salt: it’s June 2009, and Hyperspaces has been in beta for close to 6 months. Life tends to happen, and I’m sure my users are happier that I chose to give them something to play with. I’ve learnt a lot about the process though, which I’ll blog about at some point.*

With the Hyperspaces public beta coming quite soon, I’ve been thinking about how to release beta software, and when it’s appropriate to do so.

My previous piece of software - VirtueDesktops - had eternal beta syndrome (EBS). Hell, while I was running the project I’m not even sure I’d have called it a beta knowing what I do now. **This was a huge fucking mistake**. And it showed. Users got awfully upset, and the only reason I got away with it was because I didn’t charge anything for the software.

## Release your beta when you have weeks left until release - not months

How often do you download a great new piece of software that’s in beta, and then spend the next 6 months waiting for it to become stable enough for daily use? Seriously, if you couldn’t realistically release a bug-free version of your software within 4 weeks of putting out your public beta - **hold off and get your software to a point where you can!**

## Protect your reputation above all else

I believe the most important thing I have as a developer is my reputation. Skills, languages and patterns can be learnt - reputation is something that has to be earned, and is really hard to rebuild if you damage it. In my experience buggy releases or a constantly “in-beta” product are two of the fastest ways to cripple your reputation.

## If something goes wrong - make sure the user can let you know as easily as possible

This applies regardless of the release status of your application - if something goes wrong, the user will only let you know if:

1.  The error really pisses them off; or
2.  It’s incredibly easy to do so

I generally believe in collecting as much information as possible and automatically posting this back to your servers - this way, you don’t need to ask the user to root about in their Library folder. **If you’re going to do this, make sure you let the user know exactly what’s happening!**. When I was coding VirtueDesktops, I used Unsanity’s Smart Crash Reporter - and was quite happy with it. I’m still not sure what I’ll use for Hyperspaces - APE is out for Leopard now, but it’s not out of beta yet.

## Conclusion

Don’t release your software before it’s ready, and make sure it’s easy to report errors when they happen.