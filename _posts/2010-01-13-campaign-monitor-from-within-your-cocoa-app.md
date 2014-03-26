---
layout: post
title: Campaign Monitor from within your Cocoa app
tags: [Cocoa, Programming]
date: 13 January 2010 16:09:00
---

*This is the first of my ‘Giving back’ posts. The idea is that I’ll give something back to this wonderful Cocoa coding community at least once every couple of weeks. I mean, what’s the point of going indie if I can’t do what I want once in a while? :)*

<img src="http://static.tonyarnold.com/join_our_mailing_list-1306152759.png" alt="Screenshot of dialog asking to join a mailing list from CBMailingListSignup" class="center" />

Of all the marketing avenues I continue to investigate and read about, mailing lists seem to be something that the rest of you recommend time and again. I missed a few boats when I launched [Hyperspaces][2] - were I to do the launch over again, I’d make sure that a mailing list was in place and easy to join from my website and within my app. I’ve always admired the way the [Panic][3] apps ask you to join their mailing list the first time you start them - it’s simple and unobtrusive.

As part of my work toward future versions of [Hyperspaces][2], I’m looking to do the same. I’m still deciding which mailing list package/provider I will use in the end, so please don’t take this as a “this is what The CocoaBots use” post, however I did meet the [Campaign Monitor][4] guys at [Web Directions South 09][5], and their product has a nice web service API. So I put together a small example project that will sign a user up to your Campaign Monitor mailing list from directly within your app.

The code is heavily inspired by Uli’s [UKCrashReporter][6] and Wolf’s [JRFeedbackProvider][7] projects (this is like a mutant offspring of the two). I may not end up using it in my apps, but hopefully someone else finds it useful.

The GitHub project is at [http://github.com/tonyarnold/CBMailingListSignup][9], and the code is licensed under the [Creative Commons Attribution 2.5 Australia License][8].

 [2]: http://thecocoabots.com/hyperspaces/
 [3]: http://panic.com/
 [4]: http://campaignmonitor.com/
 [5]: http://wds09.webdirections.org/
 [6]: http://zathras.de/angelweb/sourcecode.htm
 [7]: http://github.com/rentzsch/jrfeedbackprovider/
 [8]: http://creativecommons.org/licenses/by/2.5/au/
 [9]: http://github.com/tonyarnold/CBMailingListSignup/