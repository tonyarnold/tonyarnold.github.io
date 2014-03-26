---
layout: post
title: "Making your iPhone app's maps work like Apple's"
tags:  [Cocoa, Programming, Sample Code, iPhone SDK]
date: 21 April 2010 17:35:00
---

***Disclaimer:** These instructions have been tested under iPhone SDK 3.1 - they will probably work under future releases of the iPhone OS, but I don't make any guarantees. **Don't ever blindly include code in your apps**.*

I've had the opportunity to work on a couple of smaller iPhone apps that include `MKMapView` components to show the location of stores and other items of interest. One of the things I found a little challenging was that the map views didn't work quite the same way as those found within Apple's Maps.app on the iPhone. I mean, sure - you can pan around the map with your fingers and zoom in and out by pinching, so the basics are there - but once you start tracking the user's current location (`showsUserLocation`) all the nice stuff just falls away.

<img src="http://static.tonyarnold.com/ttm_example-1306152825.png" alt="Screenshot of TapThatMap sample app" class="center"/>

Try it now - pop open the Maps app on your iPhone and tap the little crosshair button in the lower left corner of the map to show your current location. Straight away you'll notice that the map zooms and scrolls to centre on your current location. Now try moving the map around - the map location follows your fingers, with that pretty blue pulsing dot tailing your every move. Nice, huh? OK, now scroll the map somewhere else using your fingers. What happened? The `showsUserLocation` property just set itself to `NO` and the map stopped following you. Right thing to do, hey? Guess what - that's not standard behaviour if you just drop an `MKMapView` into your app. The good news is that it's not hard to copy this behaviour, and you don't have to use private APIs either (nice!). 

Here's how an `MKMapView` is structured at the highest levels (in a very loose sense):

	- MKMapView
	  - UIView
	    - UIScrollView

And that's what makes it nice and easy to replicate this behaviour - the `UIScrollView` has a property named `contentOffset` that we can watch for changes using Key/Value Observation. When the `contentOffset` property changes, we can quickly check if the user is making the changes (in which case we want to turn off our `showsUserLocation` property), or if something else like the application is making the changes in which case we just want to ignore the change (ie. when zooming to a specific pin due to a search).

## Sample Code

I've uploaded a sample project to Github containing a very simple implementation of this approach - you're welcome to clone it, fork it or just read through it:

<div class="center" markdown="1">
[![Xcode Project Icon][2]TapThatMap Sample for iPhone SDK][0]
</div>

Hopefully this will help someone else looking to achieve the same effect. Currently, tapping the "**Start Following Me**" button does not zoom to and centre on the user's location like Apple's Maps.app, but otherwise the functionality provided by `MapKit.framework` should be enough. I'll add more to the sample project as I get time.

 [0]: http://github.com/tonyarnold/sample-iphonesdk-tapthatmap
 [1]: http://static.tonyarnold.com/ttm_example-1306152825.png "Screenshot of TapThatMap sample app"
 [2]: http://static.tonyarnold.com/xcode_project_icon-1306152857.png "Xcode Project Icon (128px by 128px)"
 