---
layout: post
title: Chat Server for Mac OS X Client
date: 09 November 2005 15:00:00
tags: [Mac]
---

> ## Notice
>
> *Given the age of this package, I’ve decided to take it down. I cannot support a package for an operating system and processor architecture that I no longer run.*

OK, I’ve been putting this off for a while. Same as pretty much everything else I release at the moment, I make no guarantees - this package works for me, and I’ll be pleased if it works for you too. Oh, and as with everything else I’ve made so far, **it’s Tiger only, and is only compiled for PowerPC-based macs**.

## What is it?

This installer package installs the version of jabber than Apple bundles with Mac OS X Server as ‘iChat Server’. I’ve renamed it to plain ole’ ‘Chat Server’ so people don’t confuse my dodgy work with the Apple version. I’ve also added jabber transports for MSN and Yahoo! (although you’ll need to use a dedicated client like [Affinix’s Psi][1] jabber client to activate that functionality).

## How do I use it?

Run the installer, reboot, then open iChat and follow the instructions below:

1.  Open iChat, then go to “*iChat >> Preferences…*”
2.  Go to the “*Accounts*” tab, then select the “*+*” symbol at the bottom of the window to add a new account
3.  Under “*Account Type*”, select “**Jabber Account**”
4.  For Jabber ID, enter the username of the account you are currently logged in as, plus ‘**@localhost**’ – for example, my account login is ‘**tony**’, so my Jabber ID would be ‘**tony@localhost**’
5.  Set “*Server*” to ‘**localhost**’, and “*Password*” to the password of the account you are currently logged in as.
6.  Don’t forget to enter a description!
7.  Select “*Add*” – if all went according to plan, you should now be able to connect to your locally installed Chat Server!

## How do I chat to my MSN/Yahoo! buddies?

Using [Affinix’s Psi][1], set-up and connect to your local chat server (the trick is to follow iChat’s settings, but also select “Use SSL encryption (to server)” and “Allow Plaintext Login” under the “Connection” tab. Then follow these instructions:

1.  Make sure you are successfully connected to your local Chat Server
2.  Go to “*General >> Service Discovery*” and select the account you’ve just set-up
3.  You should see both “*MSN Transport*” and “*Yahoo! Transport*” – right-click on whichever one you want to use (yes, you can use both at the same time) and select “*Register*”
4.  Fill in your username and password for whichever network you just chose and hit “*Register*”
5.  If all went according to plan, you should be asked to authorise the network transport you just added - do that, then close Psi and re-open iChat
6.  Voila! You can now chat to your MSN/Yahoo! buddies directly from iChat (although you can’t send files or images to them as you do your iChat buddies)

## Enough already – where’s the download?

<strike>OK, OK, you can download it here: Install Chat Server.zip (8.9Mb). As always, let me know if you run into trouble via the comments.</strike>


 [1]: http://psi.affinix.com/
