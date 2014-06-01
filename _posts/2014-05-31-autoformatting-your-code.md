---
layout: post
title: "Automatically Formatting Your Objective-C"
date: "31 May 2014 13:22:00"
tags: 
  - Programming
  - "Objective-C"
published: true
---

One of the tenets of writing good code is keeping your code readable. This is a conversation that includes more than just the visual aesthetic of how you lay out your classes, but today I'd like to focus on that because it's something we can automate (whereas good class design is what keeps us all employed, and presently _can't_ be automated).  

Using consistent numbers of lines between common structures allows your brain to more easily pick up patterns in your code, which helps you scan the structure of your classes faster. It's also hugely beneficial when introducing a new developer to your existing code — the patterns make reading and learning your classes a much nicer experience.

_"But"_, I hear you say, _"it takes too long to worry about formatting and laying out my code! What's a few misplaced brackets going to cost me in the long run?"_ and away you go, committing inconsistently formatted code.

<img src="http://static.tonyarnold.com/picard-facepalm.jpeg" alt="Jean-Luc Picard facepalming" class="widescreen" />

What if you didn't have to do anything extra while you're actually writing your code? (sans a little initial setup)

The great news is that there are multiple tools available to help format Objective-C, but the one to watch seems to be [Clang Format][clang-format]. Given that it is integrated into the Clang toolset, there's a good chance that Apple may include it in a future release of Xcode.

Out of the box, `clang-format` is a command-line tool that you can run directly on your source files. It doesn't add/remove code from your source, instead focusing on adjusting the whitespace characters within your source to make code more consistent.

With a little bit of extra effort, you can make Clang Format available from within Xcode.

## Install ClangFormat-Xcode

[ClangFormat-Xcode][clangformat-xcode] is an Xcode plugin developed by [Travis Jeffery](https://github.com/travisjeffery) that makes Clang's format tools available within Xcode.

Travis has made the plugin available via [Alcatraz](http://alcatraz.io/). Alternately if you wish to install the plugin manually:

1. Checkout the [git repository][clangformat-xcode]
2. Build and run the `ClangFormat-Xcode.xcodeproj`
3. Restart Xcode

There will be a new menu item under *Edit &#8594; Clang Format* where you can configure and trigger automatic formatting of code in your project.

<img src="http://static.tonyarnold.com/clang-format-menu.png" alt="Xcode Edit menu showing the Clang Format menu expanded" class="widescreen"/>

You can format the current file, selected text within the current file or more than one file selected in the Xcode project navigator. I've assigned keystrokes to these using _System Preferences &#8594; Keyboard &#8594; Shortcuts &#8594; App Shortcuts_.

I find that I often leave *Enable Format On Save* enabled once I have everything configured the way I like it. This means that every time I save, my files are automatically re-formatted to my liking and I don't have to think about it — nice, right?

> I've had a few people let me know that the current build of ClangFormat-Xcode has issues formatting dictionary literals. This bug was fixed in Clang a week or two ago, and you can [download an updated build](http://static.tonyarnold.com/clang-format-20140601.zip) that I compiled today. Just place this new copy of `clang-format` in your PATH (`/usr/local/bin/clang-format` is a good spot) and then select *Edit &#8594; Clang Format &#8594; Use System ClangFormat*.

## Configure Clang Format

Clang Format has a number of styles packaged with it, including the code formatting styles used by the LLVM project, Google, Chromium, Mozilla and WebKit. All of these projects make fairly heavy use of C++, so the way they format Objective-C can be less than ideal. Thankfully, Clang Format can be configured using a `.clang-format` file containing a series of configuration options.

My `.clang-format` looks like this:

    BasedOnStyle: Chromium
    AlignTrailingComments: true
    BreakBeforeBraces: Allman
    ColumnLimit: 0
    IndentWidth: 4
    KeepEmptyLinesAtTheStartOfBlocks: false
    ObjCSpaceAfterProperty: true
    ObjCSpaceBeforeProtocolList: true
    PointerBindsToType: false
    SpacesBeforeTrailingComments: 1
    TabWidth: 8
    UseTab: Never


### Configure Globally

It's a good idea to have a global `.clang-format` configuration file — you place this in your home directory: `~/.clang-format`

### Configuration Per Project

Each project can (and should) have it's own configuration — just place a `.clang-format` file in the root of your project.

### Configuration Per Folder

It's common to include third party code in your projects that you'd prefer not to re-format accidentally. Simply put a `.clang-format` file in the directory of the files you'd prefer not to format and make it's contents:

    ---
    BasedOnStyle: None
    ...

## You Have No Excuse Now

So there you have it. There'll be times where Clang Format's output doesn't quite match what you're expecting, but it's more important to be consistent and readable than perfect. I'd love to see more projects include a `.clang-format` file so that contributors can automatically adopt the formatting style without thinking about it.

Go forth, be formatted (and let's all cross our fingers for this being included in Xcode.next!).



 [clang-format]: http://clang.llvm.org/docs/ClangFormat.html
 [clangformat-xcode]: https://github.com/travisjeffery/ClangFormat-Xcode/
