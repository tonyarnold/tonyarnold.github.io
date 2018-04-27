---
layout: post
title: MySQL Bindings for Ruby under Mac OS X Tiger
date: 12 August 2005 16:30:00
tags: [MySQL, Programming, Rails, Ruby, Web]
---

{% capture years_ago %}{{ site.time | date: "%Y" | minus:2005 }}{% endcapture %}

> ## Outdated Information
>
> The last time this post was updated, it was {{years_ago}} years old. I wouldn't recommend using the instructions below on anything but a Mac running Mac OS X 10.4 "Tiger".
>
> Also, these instructions are not for Mac OS X Server - it comes with it’s own version of MySQL installed, and thus the procedure below probably won’t work without some modifications (then again, if you’re running Server, you’re probably skilled enough to figure out what to change yourself). Apologies for anyone on Server who has tried to follow these instructions.

OK, after yesterdays mammoth post this one should be a bit quicker. Basically, there are a few issues with the building of native gems under Mac OS X at the moment, and until they’re dealt with up-stream, getting certain rubygems to install is going to be trial and error.

#### 1. Download and install MySQL

I’ll leave you to figure this out - I use the latest 5.x release myself, but version 4.x will work just as well. You can get the disk images from [MySQL.com][1]. There is also a launch daemon written by Jacob Stetser, which you can [grab from his blog][2] (I would recommend using this over the MySQL.com bundled startup item).

#### 2. Un-install any MySQL rubygems you may already have installed

We need to remove any earlier – possibly failed – attempts at installing the binding:

    $ sudo gem uninstall mysql

If all goes well, you’ll now be ruby-mysql-less.

#### 3. Download and install the latest MySQL bindings

For some reason, people have been seeing dynamic linker issues with the latest released version of the mysql bindings, but Courtenay over at [http://habtm.com/]() found that using the version 2.7 bindings resolves this issue

So go ahead and download [http://tmtm.org/downloads/mysql/ruby/mysql-ruby-2.7.tar.gz][4], I’ll wait. When you’re done, extract the archive and switch back to the terminal and `cd` to where you’ve extracted the source. The parts you need to type are in bold below.

    $ sudo gcc_select 4.0
    $ export PATH=/usr/local/mysql/bin:$PATH
    $ ruby extconf.rb --with-mysql-config
    $ make
    $ sudo make install

Guess what? If everything proceeded as above, you’re done! Next time, I’ll post some information about actually using the mysql bindings (even given my preference for sqlite). For now, [the Ruby on Rails wiki][3] has some great tutorials and starting points, as well as information about contacting other rails developers. Getting in contact with other Rails developers is something I really recommend you do, as the Rails community has some great minds you can learn from, and some friendly people who can help you when you get stuck. Good luck!

 [1]: http://www.mysql.com/
 [2]: http://blog.unquiet.net/archives/2005/05/19/launchd-item-for-mysql/
 [3]: http://wiki.rubyonrails.com/
 [4]: http://tmtm.org/downloads/mysql/ruby/mysql-ruby-2.7.tar.gz
