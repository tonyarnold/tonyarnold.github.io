---
layout: post
title: How to show the duration of builds in Xcode
date: 20 April 2016 09:15:00
tags: [Mac, Programming, Xcode]
---

<img src="http://static.tonyarnold.com/xcode-build-duration.png" alt="Xcode Toolbar showing build duration" class="widescreen" />

Ever wondered how long your builds in Xcode are taking? Here's a quick way to show them as inside Xcode after each build:

1. In your terminal, type:

```
defaults write com.apple.dt.Xcode ShowBuildOperationDuration -bool YES
```

2. Relaunch Xcode.
3. Build your project to see the duration of each build!
