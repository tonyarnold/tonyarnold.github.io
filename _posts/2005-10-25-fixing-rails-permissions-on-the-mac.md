---
layout: post
title: Fixing Rails' permissions on the Mac
date: 25 October 2005 15:30:00
tags: [Mac, Programming, Ruby, Rails, Web]
---

About three times a week, people message or email me with questions about their Rails app having permission problems. I’m posting this so people can figure this out themselves (not that I don’t appreciate the kind words that come with the questions).

    $ mkdir /Library/WebServer/Rails
    $ chgrp www /Library/WebServer/Rails
    $ cd /Library/WebServer/Rails
    $ rails ./MyWondrousRailsApp

So long as you create your Rails apps there, you shouldn’t have any problems. Basically, it looks like Rails needs read access to all of your application path – hence putting it in your home directory will result in your application throwing an error. Natch
