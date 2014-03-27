---
layout: post
title: Rolling with Ruby on Rails on Mac OS X Tiger
date: 11 August 2005 09:30:00
tags: [Mac, Programming, Ruby, Rails, Web]
---

{% capture years_ago %}{{ site.time | date: %Y | minus:2005 }}{% endcapture %}

> ## Outdated Information
>
> This post was written {{years_ago}} years ago. I wouldn't recommend using the instructions below on anything but a Mac running Mac OS X 10.4 "Tiger".

I’ve found myself helping a few people get up and running with [Ruby on Rails][1] over the last month, mainly due to my [Ruby on Rails installer package][2]. I thought it might be a good idea to document installing and setting up rails from end to end on Mac OS X, given the difficulties some people are encountering along the way.

### Prerequisites

* You should install the Xcode Tools package (it’s on your Tiger installer disc) before starting the instructions below - I’ve had reports of Rails working without the Xcode tools, but it’s just simpler to have them there anyway.
* You must not be using a custom-installed version of Ruby or Apache (i.e. via Fink or DarwinPorts), as the installer package augments the included versions that come with Mac OS X Tiger, and will not work with custom-installed binaries.
* You should be familiar with some basic terminal commands. These instructions will help, but Rails itself has components that can only be run from the command line.

### Download and install the package

First up, grab the package I mentioned above: [Ruby on Rails installer][2] (about 6.6 Mb), and install it. This package includes:

* A fix for Ruby 1.8.2 that comes with Mac OS X 10.4 - by default, it tries to cross-compile an native rubygems extensions for i686 as well as ppc. This won’t work on a standard Tiger install, so we remove those references.
* FastCGI developer’s kit
* RubyGems 0.8.10 with the following gems pre-installed:
  * BlueCloth 1.0
  * FastCGI Bindings for Ruby 0.8.6.1
  * Madeleine 0.7.1
  * Rake 0.6.2
    * RedCloth 3.0.4
    * Ruby on Rails 0.13.1
    * SQLite 3 Bindings for Ruby 1.1.0
    * Syntax 1.0.0
    * More…

### Update your rubygems

The installer package I created was built a few months ago, so some of the gems have newer versions available. Thankfully, gems are really, really easy to update. Open a new terminal window and paste this in:

    $ sudo gem update

This will go through the process of bringing all of your gems, including Rails, up to the latest versions available. Accept any questions it asks about dependencies.

### Create a test rails application

To make sure everything installed properly, go back to the terminal and type the following:

    $ cd ~
    $ mkdir Rails
    $ cd Rails
    $ rails Test

You should see the following output:

    create  
    create  app/apis
    create  app/controllers
    create  app/helpers
    create  app/models
    create  app/views/layouts
    create  config/environments
    create  components
    create  db
    create  doc
    create  lib
    create  log
    create  public/images
    create  public/javascripts
    create  public/stylesheets
    create  script
    create  test/fixtures
    create  test/functional
    create  test/mocks/development
    create  test/mocks/test
    create  test/unit
    create  vendor
    create  Rakefile
    create  README
    create  CHANGELOG
    create  app/controllers/application.rb
    create  app/helpers/application_helper.rb
    create  test/test_helper.rb
    create  config/database.yml
    create  config/routes.rb
    create  public/.htaccess
    create  config/environment.rb
    create  config/environments/production.rb
    create  config/environments/development.rb
    create  config/environments/test.rb
    create  script/console
    create  script/destroy
    create  script/generate
    create  script/server
    create  script/runner
    create  script/benchmarker
    create  script/profiler
    create  script/breakpointer
    create  public/dispatch.rb
    create  public/dispatch.cgi
    create  public/dispatch.fcgi
    create  public/404.html
    create  public/500.html
    create  public/index.html
    create  public/favicon.ico
    create  public/javascripts/prototype.js
    create  public/javascripts/effects.js
    create  public/javascripts/dragdrop.js
    create  public/javascripts/controls.js
    create  doc/README_FOR_APP
    create  log/server.log
    create  log/production.log
    create  log/development.log
    create  log/test.log

If that all worked, congratulations! You now have a working rails install. At this point, you could simple type:

    $ cd ~/Rails/Test
    $ ./script/server

And rails will bring up WEBrick, a simple ruby-based web server that you can use to develop with. You’ll notice that WEBrick is slow - which is why we’re going to use Apache instead.

### Setting the right permissions on your application

If your rails application is still running WEBrick, stop that now by pressing control-c. There are a couple of ways to do set-up rails applications under Apache, but I’m going to stick with what I consider to be the most straight-forward approach. Your applications will be served under URLs like http://localhost/testapp/.

First up, we need to make sure that the permissions on your rails application are OK. This is the most common error I’ve come across when setting up a new application. It’s important to know which user the Apache is running as - by default under Mac OS X, it’s the user `www` with a group of `www`. Obviously, you still need to be able to write to your application, so we’re just going to change the group on the applications files by typing:

    $ cd ~/Rails/
    $ sudo chgrp -R www Test

Now we need to make sure that the `db`, `log`, and `public`, and any logs stored in `log` can be accessed and written to by Apache:

  $ cd ~/Rails/Test
  $ chmod 0775 db
  $ chmod 0777 log
  $ chmod 0775 public
  $ chmod 0666 log/*.log

Right, your permissions should be OK at this point, so let’s move on to configuring Apache to see your rails application!

### Set-up Apache to handle your rails applications

In your favourite text editor (I use [Macromate’s TextMate][3]) open up `/etc/httpd/httpd.conf`. Scroll right to the bottom and make sure the following code is present:


    <IfModule mod_fastcgi.c>
        FastCgiIpcDir /tmp/fcgi_ipc/
        AddHandler fastcgi-script .fcgi
    </IfModule>


Now you’ll need to add the code to handle your application:


    Alias /test/ "/Users/YOURUSERNAME/Rails/Test/public/"
    Alias /test "/Users/YOURUSERNAME/Rails/Test/public/"

    <Directory /Users/YOURUSERNAME/Rails/Test/public/>
        Options ExecCGI FollowSymLinks
        AllowOverride all
        Order allow,deny
        Allow from all
    </Directory>


Save and close the file. Now inside your `Test` rails application, you’ll need to open `public/.htaccess` and change the following line:

    RewriteRule ^(.*)$ dispatch.cgi [QSA,L]

to

    RewriteRule ^(.*)$ dispatch.fcgi [QSA,L]

You’ll also need to add the following line underneath `RewriteEngine On`:

    RewriteBase /test/

Save and close the file. Now, type the following in your terminal:

    $ sudo apachectl graceful

### Check your application

Open your web browser and point it at [http://localhost/test/][4]. If everything worked OK, you should be rolling on rails!

I’ll try to post some more information about where to go from here, and also how to install the mysql ruby bindings which can be troublesome, and aren’t included in my package (I use sqlite as my database while developing). For now, have fun!

 [1]: http://www.rubyonrails.com/
 [2]: /2005/12/14/ruby-on-rails-1-installer-for-mac-os-x-tiger.html
 [3]: http://www.macromates.com/
 [4]: http://localhost/test/
