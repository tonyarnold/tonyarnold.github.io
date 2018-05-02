---
layout: post
title: Showing a background color in an NSView
date: 27 April 2018 21:50:00
tags: [Mac, Programming, Tips, Xcode]
---

I've heard many a developer making the transition back to using AppKit after working with UIKit lament the lack of a `backgroundColor` property on `NSView` like that found on `UIView`.

There are two ways I'd recommend:

## Use an NSBox

`NSBox` has a `fillColor` property, and (when it is configured appropriately) it can be used to display a background fill color.

```swift
let box = NSBox(frame: .zero)
box.borderType = .noBorder
box.boxType = .custom
box.titlePosition = .noTitle
box.fillColor = .red
```

If you just need to get up and running, using `NSBox` is by far the easiest option.

## Use the view's backing layer

It's important to remember that `NSColor` is dynamic - it can and will change based upon the context it is used within - so it is important that you don't just set the background color of the view's `layer` property and never update it.

In addition, if you choose to use the view's layer to display a background color, you must ensure that the view has it's own backing layer by returning `true` from `NSView.wantsUpdateLayer`.

Here's how to do it properly:

```swift
class FillableView: NSView {
  var fillColor: NSColor {
    didSet {
      needsDisplay = true
    }
  }

  override var wantsUpdateLayer: Bool {
    return true
  }

  override func updateLayer() {
    super.updateLayer()
    layer?.backgroundColor = fillColor
  }
}
```
