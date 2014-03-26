---
layout: post
title: "My Backup Setup"
tags:  [Backup, Life, Mac]
date: 22 April 2011 22:27:00
---
After the gushing "[Thankyou, Backblaze][thanksbb]" post from earlier today, I thought it might be of some interest to others how I backup my Mac (like an elephant — hooo, I tied in a photo of my travels again!).

![Elephants have long memory. Like a backup. And a boss.][elephant]

I consider backing up to be common sense these days. If you use your Mac for work or for play, you have information that you'd be upset were it to disappear. Not backing up is the computing equivalent of driving without a seatbelt: you might not have an accident today, but you'll be thankful for it when you do.



I have four levels of backups setup — that might sound a bit excessive, but I've found some services are better suited to looking after different types of information:

### [Dropbox](http://db.tt/hsOUhWJ)

Dropbox is the centre of my backup strategy. My most important work-related documents all live in my Dropbox. I have a 50Gb account, of which I use about 5% for all of my client data, business records and any personal documents. I don't store my Music, my Movies or any non-document content with Dropbox. With the advent of Xcode 4 and defaulting to storing intermediate build files in *~/Library/Developer/Xcode/Derived Data*, I can safely leave these here without causing constant uploads. FYI, that's a referral link to Dropbox's website — if you end up signing up for a Dropbox account, I get 250Mb of free space in my account). You can use 2Gb of storage with Dropbox for free, which is *awesome*.

### [Github](http://github.com/)

If I'm working on a development project for you, or for myself, I have a private git repository setup for it on Github. This is an absolute no-brainer — the setup is simple, the user interface is simple and the support is great. For ~$7 (less if you're transacting in AUD) every programmer should have this (or the equivalent for your DVCS of choice — I've also heard good things about [Atlassian's BitBucket](https://bitbucket.org/)).

### Time Machine

1Tb external hard drives retail for about $90. Buy one, and setup Time Machine. Time Machine is far from perfect, but it's something you don't have to think about it — it just sits in the background and copies your changes to an external disk once an hour. It's also a heck of a lot quicker to restore files to your Mac from a disk that's directly attached than from any online service.


### [Backblaze](http://backblaze.com/)

AKA "The Best $5 I Spend Each Month". Backblaze sits in the background just like Time Machine, but it pushes your information up to Backblaze's data centre for long term storage rather than to local storage. It took a long time to perform the initial backup, but now that first run has finished I don't notice it at all (and it's [saved my bacon][thanksbb]) after only a couple of months of use!). The brilliant feature that Backblaze offers is that they will send you a physical hard disk containing your data should you ever need it. They also don't set limits on the amount of data you can store with them, so you don't need to cherry-pick what you'll backup — just let it do everything!


If you want to keep reading about backups, there's plenty of great info on other approaches at the [World Backup Day site](http://www.worldbackupday.net/).


 [elephant]: http://static.tonyarnold.com/elephant-1306151150.png "Elephants have long memory. Like a backup. And a boss."
 [thanksbb]: /mac/work/2011/04/22/thankyou-backblaze.html