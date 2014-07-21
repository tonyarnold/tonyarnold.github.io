---
layout: post
title: Working with NSNotFound in Swift
date: 21 July 2014 11:43:00
tags: [Swift, Programming, Learning]
---

> Disclaimer: This information is current as of Xcode 6.0b3, and is subject to change in future seeds. Also, I — like everyone outside Apple — am still learning Swift. Please, [let me know if I've missed something](https://twitter.com/tonyarnold/)!

---

**Update:** About 35 seconds after I posted this, @mattyohe [pointed out that this is exactly what Swift's optionals are for](https://twitter.com/mattyohe/status/491054206795923456). I expect that `NSNotFound` will disappear at some point in the next few years.

The class ended up looking like this:

{% highlight swift %}
class ImagePageContentViewModel
{
    var image: UIImage
    var index: Int?

    init(image:UIImage, atIndex index:Int?)
    {
        self.image = image

        if let index = index
        {
            self.index = index
        }
    }

    convenience init(image:UIImage)
    {
        self.init(image:image, atIndex:.None)
    }
}
{% endhighlight %}

`NSNotFound` is currently a common way for Cocoa frameworks to indicate that a result couldn't be found when searching through indices and other serial data. I wanted to create a simple Swift class to represent the data behind a cell that displays an image, like so:

    class ImagePageContentViewModel
    {
        var image: UIImage
        var index: Int

        init(image:UIImage, atIndex index:Int = NSNotFound)
        {
            self.image = image
            self.index = index
        }
    }

Unfortunately, I ran into a few errors that didn't have  obvious solutions (at least to me!) from the outset.

Straight up, if you've tried to use `NSNotFound` in Swift you've probably hit a few stumbling blocks. If you create the class above in your project, you'll see an error — **Ambiguous use of 'NSNotFound'**. To fix this, you'll need to be more explicit about where `NSNotFound` is coming from — easy enough, [as described by Erica Sadun](http://ericasadun.com/2014/06/13/swift-fixing-ambiguous-use-of-nsnotfound/) just use `Foundation.NSNotFound` instead.

    init(image:UIImage, atIndex index:Int = Foundation.NSNotFound) {
        // ...
    }

Next, you'll see Swift get a little tripped up trying to convert from an `NSInteger` to an `NSNumber` and then back to an `Int` again — the error this time is **'NSNumber' is not a subtype of 'Int'**. In this class, I wanted to use pure Swift types as much as possible while maintaining Cocoa-isms like NSNotFound, so the `index` parameter is defined as an `Int`.

> I'm sure there's a pragmatic argument to be made for just defining this parameter as an NSNumber and wiping your hands of the problem, but I'm being idealistic in my adoption and learning of Swift so assume that I really want this parameter to be an Int.

It's pretty easy to give Swift hints about the types you'd like things to resolve to, and you'll probably need to do this a bit with numbers. In this instance, we'll explicity force this number to be an `Int`:

    init(image:UIImage, atIndex index:Int = Int(Foundation.NSNotFound)) {
        // ...
    }

This compiles and works as you'd expect. I can now call either:

    let viewModel = ImagePageContentViewModel(image: myImage)

or

    let viewModel = ImagePageContentViewModel(image: myImage, index: 6)

I don't have enough experience with Swift yet to know if the conversion of an enumerable type in Objective-C to C should require wrapping in `Int()` so I've not filed this as a radar.
