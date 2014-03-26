---
layout: post
title: "Xcode syntax highlighting fix"
tags:  [Cocoa, Programming]
---

Over the last couple of months of use of Xcode 4, I've found that (at times) everyone's favourite Objective-C IDE loses its way while making code pretty and colourful. I've filed radars about it, but I could never reliably and consistently reproduce the problem so the Xcode gnomes at Apple couldn't either.

If you're having trouble with syntax highlighting in your Xcode projects, please try this tip from [Lars Schneider][1]:

1. Increase the indexing log level by opening Terminal.app and executing the following command:

    `defaults write com.apple.dt.Xcode IDEIndexingClangInvocationLogLevel 3`

2. Open Console.app and search for "**Xcode**" — specifically for "file not found" errors for header files mentioned in your PCH (Pre-Compiled Header)
3. Fix any problems that are reported in the console logs.

Lars mentions adding "`$(SRCROOT)/**`" to your project header search paths in his answer, but I didn't find that to be necessary.

The good news is that Xcode 4.2 seems to improve this situation (and a bunch of others), so grab a copy when it's released later this week.

Thanks to [Rafif Yalda for pointing me in the direction of Lars' Stack Overflow post this morning][2]!

 [1]: http://stackoverflow.com/questions/2138047/xcode-code-loses-syntax-coloring/7676487#7676487
 [2]: https://twitter.com/rafifyalda/status/123154154842632192
