---
layout: post
title: Ruby on Rails for PowerPC macs
date: 09 October 2005 20:00:00
tags: [Mac, Programming, Web]
---

> ## Notice
>
> *Given the age of this package, I've decided to take it down. I cannot support a package for an operating system and processor architecture that I no longer run. Under Mac OS X 10.5 and later, Ruby on Rails is included in the default install.*

Well fellow fat controllers, after much feedback and a fair amount of procrastination, here is an updated copy of my ruby on rails installer package. It now contains the latest versions of rails, rake and a number of other useful gems. As always, a ‘`sudo gem update`’ wouldn’t hurt after installing this package.

On another note, I’ve been told that my previous package was missing the SWIG bindings, so users without the Xcode tools couldn’t use a minimal rails install and sqlite3 to get started (I can understand wanting to do this - the Xcode tools are getting quite hefty!). Well, this release includes the SWIG bindings (hence it being double the size). I’ve not tested this without the Xcode tools, so if some adventurous soul could let me know how this goes, I’d be mighty appreciative.

As always, this package **does not contain the MySQL ruby bindings**. You can [follow my earlier instructions to install the MySQL bindings][1] if you feel you need them installed.

**Update:** It appears that this installer **will** let you use Ruby on Rails without the Xcode tools installed. Be aware that you won’t be able to install any rubygems that contain a native extension (like the MySQL bindings) due to the need for a compiler. You will also not be able to upgrade some of your rubygems for the same reason. It will get you off the ground though, and if Ruby on Rails gets your attention, installing the Xcode tools won’t seem like such a big deal! It is also compiled for PowerPC only.


 [1]: /entries/mysql-bindings-for-ruby-under-mac-os-x-tiger
