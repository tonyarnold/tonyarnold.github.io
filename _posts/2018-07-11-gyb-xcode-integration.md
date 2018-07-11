---
layout: post
title: Integrating GYB with Xcode
date: 11 July 2018 22:30:00
tags: [Mac, Programming, Tips, Xcode]
---

NSHipster posted a great article on [using GYB to reduce boilerplate in your Swift projects](https://nshipster.com/swift-gyb/), but I found the suggestion of how to integrate with Xcode via a Build Phase a bit loose and messy (at least in terms of littering your project directory with generated files).

I'd suggest you have a look at creating a custom Build Rule instead - this will have the advantage of outputting the generated Swift files to a directory outside of your project (therefore leaving your Git status clean during CI and other automated processes).

Here's what you need to do:

1.  Do exactly as [Mattt suggests in his article](https://nshipster.com/swift-gyb/#using-gyb-in-xcode) and download the GYB scripts into your project directory:

    ```sh
    $ mkdir Scripts
    $ cd Scripts
    $ wget https://github.com/apple/swift/raw/master/utils/gyb
    $ wget https://github.com/apple/swift/raw/master/utils/gyb.py
    $ chmod +x gyb
    ```

2.  In Xcode, select your project, then the target you wish to use GYB files with, then select the _Build Rules_ tab.
3.  Use the small _+_ button to add a new Build Rule, then configure it as follows:

    - Process **Source files with names matching:** `*.gyb`
    - Using **Custom script:**, using the following script:

      ```sh
      "${PROJECT_DIR}/Scripts/gyb" --line-directive '' -o "${DERIVED_FILE_DIR}/${INPUT_FILE_BASE}" "${INPUT_FILE_PATH}"
      ```

    - Add one entry to **Output Files**:

      ```sh
      $(DERIVED_FILE_DIR)/$(INPUT_FILE_BASE)
      ```

4.  Create a new GYB file in your project - remember that it **must** have a file extension of `.swift.gyb`
5.  Add the new GYB file to your target's _Compile Sources_ phase.
6.  Add `Scripts/gyb.pyc` to your `.gitignore` file.
7.  Build your project. You can check that the output of your GYB is as you expect by navigating to the `DERIVED_FILE_DIR` directory. This is usually some variation of the following:

    ```
    ~/Library/Developer/Xcode/DerivedData/YOURPROJECT-ID/Build/Intermediates.noindex/YOURPROJECT.build/Debug/YOURTARGET.build/DerivedSources/
    ```

8.  That's it! Commit your changes and get started replacing your boilerplate with automated GYB files.

> **Alternatives:** You could consider integrating Krzysztof Zabłocki's [Sourcery](https://github.com/krzysztofzablocki/Sourcery) instead of GYB - it provides much the same result in a similar template format, but has a bunch of well document examples and tutorials available.
