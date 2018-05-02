---
layout: post
published: true
title: How to create a grid of CALayers
tags:
  - Cocoa
  - Programming
date: "14 December 2007 00:37:00"
---

*Update: this is indeed a dodgy method I’ve posted below. I’ll update this post when I can, but you’re better off digging out your 8th grade maths and working out the coordinates of surrounding cells and constraining all edges to each other. Friends don’t let friends blog at 12.30am.*

So I’ve been puzzling for a few weeks through the dim and darkened alleyways of [Leopard’s new Core Animation APIs][1] and the rather wonderful CALayer. One of the features I’m planning for [Hyperspaces][2] is a desktop pager that will show basic approximations of your on-screen windows - sort of like what used to be in VirtueDesktops, but way cooler because it will use Core Animation to smoothly animate changes in state.

Unfortunately, I hit a rather interesting problem while attempting to draw a grid of self-positioning CALayers. See, you can tie CALayers together using constraints, but in a traditional grid of objects you need to tie all the edges of the grid objects to each other (and the outer grid objects to the frame of the constraining frame) - but you can’t constrain CALayers using CALayers that haven’t been created yet (still with me? sounds sane, right?).

<img src="http://static.tonyarnold.com/calayer_grid_example-1306152218.png" alt="CALayer grid example" class="center" />

So the answer turned out to be to cheat. First, constrain the width and height of all CALayer grid objects to be consistently based on the height and width of the constraining CALayer (scaled to fit the number of columns and rows we’re trying to get onscreen). Tie all the “outer” CALayers to the constraining CALayer on the edges where they connect with it. Now, tie the left and top edges of all CALayers to the right and bottom edges of the CALayers around them as shown to the left.

So in the interests of getting more Core Animation code out there, here is my somewhat dodgy, but completely re-usable approach to drawing a grid of CALayers in your own monstrosity of an application. I’m open to being completely corrected by someone willing to write a proper CALayoutManager for this. [Neil][4], [James][5] - now that you’ve been through Cocoa bootcamp, I expect to see some really inappropriate Core Animation, OK? Use this as a starting point:

{% highlight obj-c %}
NSRect pagerViewFrame = [pagerView frame];
pagerLayers = [[NSMutableArray alloc] init];

CALayer* mainLayer = [pagerView layer];

CALayer *constraintLayer = [CALayer layer];
[pagerView setLayer:constraintLayer];
[pagerView setWantsLayer:YES];
constraintLayer.bounds = mainLayer.bounds;
constraintLayer.name = @"constraintsLayer";
constraintLayer.anchorPoint = CGPointMake( 0.5, 0.5 );
constraintLayer.autoresizingMask = (kCALayerWidthSizable|kCALayerHeightSizable);
constraintLayer.backgroundColor = [NSColor blackColor].CGColor;
constraintLayer.position = CGPointMake( 0, 0 );
constraintLayer.contentsGravity = kCAGravityResizeAspect;
constraintLayer.masksToBounds = YES;
constraintLayer.layoutManager = [CAConstraintLayoutManager layoutManager];

// Initialization code here.
HSSpaces *spacesInfo = [HSSpaces sharedInstance];

float itemWidth = (pagerViewFrame.size.width / [spacesInfo.columns floatValue]);
float itemHeight = (pagerViewFrame.size.height / [spacesInfo.rows floatValue]);
float currentRow = -1;
float currentColumn = 0;


for (HSSpace *space in spacesInfo.spaces) {

  if ( [space.number intValue] % [spacesInfo.columns intValue] == 0 ) {
    currentRow++;
    currentColumn = 0;
  }

  // We need to calculate whether we are:
  //  a) Dealing with an edge
  //    i) Right?
  //    ii) Left?
  //    iii) Top?
  //    iv) Bottom?

  BOOL isRightEdge = (currentColumn == ([spacesInfo.columns floatValue] - 1));
  BOOL isLeftEdge = (currentColumn == 0.0f);
  BOOL isTopEdge = (currentRow == 0.0f);
  BOOL isBottomEdge = (currentRow == ([spacesInfo.rows floatValue] - 1));

  CGFloat x = itemWidth * currentColumn;
  CGFloat y = constraintLayer.bounds.size.height - (itemHeight * currentRow);

  CALayer *spaceLayer = [CALayer layer];
  spaceLayer.name = [NSString stringWithFormat:@"SpaceLayer%@", space.number];
  spaceLayer.bounds = CGRectMake( 0, 0, itemWidth, itemHeight );
  spaceLayer.position = CGPointMake( x, y );
  spaceLayer.borderColor = [NSColor yellowColor].CGColor;
  spaceLayer.borderWidth = 2.0;

  if (space.color != nil) {
    spaceLayer.backgroundColor = space.color.CGColor;
  } else {
    spaceLayer.backgroundColor = [NSColor blackColor].CGColor;
  }

  [constraintLayer addSublayer:spaceLayer];

  currentColumn++;


  // Set-up constraints
  [spaceLayer addConstraint:
    [CAConstraint constraintWithAttribute:kCAConstraintHeight
                               relativeTo:@"superlayer"
                                attribute:kCAConstraintHeight
                                    scale:(1.0 / [spacesInfo.rows floatValue])
                                    offset:0.0]];

  [spaceLayer addConstraint:
    [CAConstraint constraintWithAttribute:kCAConstraintWidth
                               relativeTo:@"superlayer"
                                attribute:kCAConstraintWidth
                                    scale:(1.0 / [spacesInfo.columns floatValue])
                                    offset:0.0]];

  // Minimum X
  if (isLeftEdge) {
    [spaceLayer addConstraint:
        [CAConstraint constraintWithAttribute:kCAConstraintMinX
                                   relativeTo:@"superlayer"
                                    attribute:kCAConstraintMinX]];
  } else {
    [spaceLayer addConstraint:
        [CAConstraint constraintWithAttribute:kCAConstraintMinX
                                   relativeTo:[NSString stringWithFormat:@"SpaceLayer%i",([space.number intValue] - 1)]
                                    attribute:kCAConstraintMaxX]];
  }

  // Maximum X
  if (isRightEdge) {
    [spaceLayer addConstraint:
        [CAConstraint constraintWithAttribute:kCAConstraintMaxX
                                   relativeTo:@"superlayer"
                                    attribute:kCAConstraintMaxX]];
  }

  // Minimum Y
  if (isBottomEdge) {
    [spaceLayer addConstraint:
        [CAConstraint constraintWithAttribute:kCAConstraintMinY
                                   relativeTo:@"superlayer"
                                    attribute:kCAConstraintMinY]];
  }

  // Maximum Y
  if (isTopEdge) {
    [spaceLayer addConstraint:
        [CAConstraint constraintWithAttribute:kCAConstraintMaxY
                                   relativeTo:@"superlayer"
                                    attribute:kCAConstraintMaxY]];
  } else {
    [spaceLayer addConstraint:
        [CAConstraint constraintWithAttribute:kCAConstraintMaxY
                                   relativeTo:[NSString stringWithFormat:@"SpaceLayer%i",([space.number intValue] * (currentRow - 1))]
                                    attribute:kCAConstraintMinY]];
  }

}
{% endhighlight %}


 [1]: http://www.apple.com/macosx/technology/coreanimation.html
 [2]: /projects/hyperspaces/
 [4]: http://neilang.com/
 [5]: http://jamespamplin.com/
