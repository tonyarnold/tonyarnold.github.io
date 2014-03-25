---
layout: post
date: 2013-12-11 10:04:00
title: Macros and portable code
published: false
---

In a lot of my projects, I have a standard utility header and implementation that I import. It's not a class, it's just a very small collection of useful macros and functions that I've written over the years. If you're keen for a copy, [go right ahead](https://github.com/thecocoabots/energon).

I often struggle with the fine line between writing code that uses only what's available with the provided SDK (UIKit/AppKit), and bringing in dependencies to make things easier.
