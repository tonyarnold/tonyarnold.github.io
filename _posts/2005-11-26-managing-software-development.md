---
layout: post
title: Managing software development
date: 26 November 2005 07:00:00
tags: [Programming, Work]
---

I’m only new at a lot of this, so go easy on me :)

I’m looking for ways to best manage the development and release cycle of Virtue and any other apps I have on the boil. At present, I use what I know - coding and compilation is done in Xcode, I manage all my code using Subversion, and I track issues (personally, it isn’t publicly available) using Trac. This works pretty well for me, but there are still things that bug me:

* **Xcode’s speed:** granted Virtue does what certain [other people have been saying is a bad idea][1] - it is composed of three frameworks, a carbon bundle, a static library and the application itself. I plan on taking a good hard look at this come the 0.6 development cycle.
* **Xcode’s subversion support:** it seems flaky… that could just be me though…
* **Release versioning:** At present, each build I release in the 0.5 cycle is automatically stamped with the current revision from my subversion repository. I’m not sure this is a great idea given the number of components, but it’s working so far (except when I want to do an official release, then I need to change the versions manually in the plist). Should I consider dropping versions for development builds entirely?
* **Release distribution and notification:** Well, if you’ve been following my releases here, you’ve been getting the whole show. Personally, I don’t want to be making releases on my blog – especially development releases. I’d love to set-up an appcast, but I haven’t found the time - can anyone recommend a product?

If anyone has suggestions or ideas (or even just the words ‘Hi!’), please post away - I’d love feedback!

 [1]: http://wilshipley.com/blog/2005/11/frameworks-are-teh-suck-err.html
