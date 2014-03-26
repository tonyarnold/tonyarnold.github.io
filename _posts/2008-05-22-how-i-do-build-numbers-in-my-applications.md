---
published: false
layout: post
title: How I do build numbers in my applications
tags: [Cocoa, Programming]
date: 22 May 2008 18:49:00
---

In my Cocoa-based developments, I like to use two version numbers in my apps:

1.  The “marketing” version - ie. “1.0”;
2.  The repository commit number, or “build” number ie. “325”;

The repository commit number is really there to aid me while I’m seeding development versions of my apps - I don’t want to have to make ridiculous versions (“1.1.0.1.0” anyone?) to ensure updates are distributed properly. I also aim for simple version numbers that my users can see and remember easily - I don’t believe in anything more than 3 levels of version numbers in a released app:

1.  The major version - ie. 1.x.x, 2.x.x, 3.x.x;
2.  The minor version - ie. x.1.x, x.2.x, x.3.x;
3.  The patch version - ie. x.x.1, x.x.2, x.x.3;

Unless you have a patch version, don’t show the third digit - just this one digit can change the entire perception a user has of your app! How simple your application is is judged on so many levels - **your version number is a part of your user interface!**

So - here’s how I do it:

## “Marketing” versions are manual

Yep, you read it right. There’s not point automating these - in my opinion, marketing is about tailoring or altering people’s perceptions of things, and so is your version number. How often do you see big companies skipping entire version numbers to alter the user’s perception of how large an upgrade they are about to buy?

There’s a couple of different ways to achieve this, but in my experience adding a user-defined build variable to your project will save you some time. Here’s how:

1.  In your Xcode project, double-click the blue project document icon at the very top of your “Groups & Files” list;
2.  A new window will open - I’ll refer to this as the “project information window”;
3.  Select the “Build” tab;
4.  At the top of the new tab, ensure that “Configuration” is set to “All Configurations”;
5.  At the bottom of the project information window, select the pop-up menu with a little gear on it and then select “Add User-Defined Setting”;
6.  Set the title of the setting to `MARKETING_VERSION`, and enter something simple as the value (ie. “1.0 alpha”);
7.  Close the project information window;
8.  Back in your Xcode project window, find and open your application’s `Info.plist` file;
9.  Modify or add the following fields as below: 
    *   **CFBundleGetInfoString**: `${MARKETING_VERSION} (Build ${REPO_VERSION}), Copyright 2008 The CocoaBots`
    *   **CFBundleShortVersionString**: `${MARKETING_VERSION} (Build ${REPO_VERSION})`
    *   **CFBundleVersion**: `${REPO_VERSION}`
10. Close your `Info.plist`;

We’ll get to `$REPO_VERSION` in a minute, but understand now that Xcode is going to automatically substitute whatever variables you enter here with their values at build time. Adding user-defined build flags to your project will add these flags as environment variables when you’re building your project.

## Your repository version numbers

I currently use [Subversion][1] as my Source Control Management (SCM) system with my projects, primarily because it’s well supported by Xcode 3, and my web host ([Dreamhost][2]. You can easily customise my scripts below to support your SCM of choice - it’s so easy!

1.  Right-click your target under the “Targets” item in your Xcode project and select “Add > New Build Phase > New Run Script Build Phase”;
2.  Set the “Shell” field to “/usr/bin/python”;
3.  Paste the following into the “Script” field:

    import re
    import os
    from Foundation import NSMutableDictionary
    
    version = os.popen4("/usr/bin/env svnversion")[1].read()
    p = re.compile('^([0-9]+)')
    shortversion = p.match(version).group()
    print "Version: " + shortversion
    info =  os.environ['BUILT_PRODUCTS_DIR']+"/"+os.environ['WRAPPER_NAME']+"/Contents/Info.plist"
    
    plist = NSMutableDictionary.dictionaryWithContentsOfFile_(info)
    plist['CFBundleVersion'] = shortversion
    plist['CFBundleShortVersionString'] = os.environ['MARKETING_VERSION'] + " (Build " + shortversion + ")"
    plist['CFBundleGetInfoString'] = os.environ['MARKETING_VERSION'] + " (Build " + shortversion + "), Copyright 2007-2008 The Cocoabots"
    plist.writeToFile_atomically_(info, 1)
    

## Trying it out

Now you should be able to close the “Run Script” window, and build your project. Take a look at the version numbers by selecting it in the Finder - you should now see your nicely integrated build numbers! It really is that simple - from here on out, whenever you make a commit and rebuild, Xcode will automatically increment according to the reported repository version. The only caveat I’ve found is that you may need to use Xcode’s “SCM > Update Entire Project” menu (or run `svn up` from the command-line) before rolling a release build - otherwise the correct repository version is not reported.

Finally, if you’re happy with what you’re seeing **commit your project!**

 [1]: http://subversion.tigris.org/
 [2]: http://dreamhost.com/