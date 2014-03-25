---
layout: post
date: 2013-08-24 10:29:00
title: Contributing Cocoa open source in a meaningful way
published: false
---

In a strangely fortuitous sequence of events, Saul had asked me to talk with him about open source projects on [NSBrief](http://nsbrief.com) next week, and then this morning I received an email from Craig at [Ink Mobility](http://inkmobility.com) asking for advice on effectively contributing open source code and projects.

This is an interesting and relevant topic given the amount of open source projects I rely on for the apps I build for clients and for myself. Vibrant, active projects like [AFNetworking] [AFNetworking], [ReactiveCocoa][ReactiveCocoa] and (ahem) [MagicalRecord] [MagicalRecord] don't just happen — they're carefully curated.

> we're looking for advice on the best way to contribute and support this [our] code for the benefit of the community

Here's the advice I gave Craig:

I guess this comes down to a few factors:

1. **The resources you have have available to support the code you release in terms of people, time and knowledge**. If you look at the more successful open source projects like [AFNetworking] [AFNetworking] and [ReactiveCocoa][ReactiveCocoa], they have a primary maintainer supported by a number of interested parties from within and without the companies where the projects originated. Contrary to popular belief open source projects do not maintain themselves in the absence of strong leadership.

2. Politics destroy open source projects. **Shut down ownership and power struggles quickly and openly, and keep an open mind to suggestions from users and contributors to your projects**. That being said, the successful open source projects have a clear “primary” owner but it’s not something that’s set in stone. Imposing your internal structures on open source projects is a sure way to see the project wither and die as your tech lead(s) get busy with commercial work internally.

3. Don’t impose unnecessary restrictions on how and when people can contribute. [Square][Square] produce some of the best open source projects, but contributing pull requests requires you to sign legal disclaimers — I don’t know many developers who are comfortable doing that. **The higher you set the barrier to entry for contributing changes, the less likely people are to just jump in and help solve problems**.

4. **Do not ever publicly ridicule another project, developer or contribution**. Even if your library is light years ahead of the competition, it reflects really poorly on you as a developer to do so. It’s fine to talk about what features make your library/app great, or to compare your project and another project — but do so from a purely factual perspective. This is basically the “Don’t be a dick” item on the list :)

5. **Be OK with someone forking your code and doing things with it you wouldn’t have done and don’t want**. It’ll happen, and how you handle this situation will determine how your project is perceived in the long run.


In terms of the more practical aspects:

1. Use a rigid approach to managing the repository for your projects. The master branch should contain only the most recent released version of your project. Keep all upcoming changes in develop and feature branches until they are ready to merge and release. You’d be surprised how many people use only a master branch, or misuse a master branch alongside a development branch — it really will save you massive amounts of time knowing you can be working on the next major revision to your project, while still fixing minor issues in your released code without having to jump through hoops to do so. I use git-flow on the projects I’m involved in to automate a lot of this workflow: [http://nvie.com/git-model/](http://nvie.com/git-model/)

2. Handle issues and pull requests as quickly and as openly as you can — with MagicalRecord, the three core contributors (Saul, Stephen and I) all have day jobs that can be very demanding. For the last few months, we’ve let the issues pile up. This reduces developer confidence in a project — nobody is going to use code that looks unmaintained. It’s also likely to take us weeks to get back on top of the list of issues to a point where it’s manageable again.

Beyond that, I’d say that **communication is the most important aspect of any successful project**. I’ve been involved in a few projects over the years and the most common mistake I’ve seen is not communicating (although that could be said of anything in life, really).


 [AFNetworking]: http://afnetworking.com
 [ReactiveCocoa]: https://github.com/reactivecocoa/reactivecocoa
 [MagicalRecord]: https://github.com/magicalpanda/MagicalRecord
 [Square]: http://github.com/square/
