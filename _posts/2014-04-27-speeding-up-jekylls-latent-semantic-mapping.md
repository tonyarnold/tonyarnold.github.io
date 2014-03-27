---
layout: post
title: Speeding up Jekyll's Latent Semantic Mapping on OS X
date: 27 March 2014 14:55:00
tags: [Web, Fix, Jekyll, Mac, Ruby, Rubygems]
---

Running Jekyll with Latent Semantic Indexing (or LSI) on a site of only 20-30 pages can take 5-10 minutes on a reasonably powerful Mac. I got tired of having to wait or isolate individual posts to get on with writing, so I took Jekyll's recommendation and tried to install the [GNU Scientific Library](http://www.gnu.org/software/gsl/) (or GSL).

It was a bit of a disaster. GSL itself installs just fine via [Homebrew][brew], but the `rb-gsl` ruby gem and many of it's dependencies would not compile.

So, doing what I always do, I stayed up far too late and fixed the problems. After properly installing GSL on my MacBook Pro, **building my site went from over 5 minutes for a site with about 100 posts, to under 5 seconds**.


## Prerequisites

 - You're using or want to use Jekyll's LSI and related posts function
 - [Xcode][xcode] (and most likely the command-line tools)
 - [Homebrew][brew]
 - Ruby, RubyGems and Bundler

## Instructions

1. Install GSL via homebrew:

        $ brew install gsl

2. If you don't already have a `Gemfile` for your Jekyll site, create one that looks similar to this:

        source 'https://rubygems.org'

        gem 'jekyll'
        gem 'narray', :git => "https://github.com/tonyarnold/narray"
        gem 'gsl', :git => "https://github.com/tonyarnold/rb-gsl"

    > **Note:** If you already have a Gemfile, the important lines are `narray` and `gsl`. Be sure to include the git repository links, as these contain my fixes to compile on OS X 10.9 "Mavericks".

3. Now use Bundler to install the dependencies on your Mac:

        $ cd {YOUR SITE'S FOLDER}
        $ bundle install

    > **Note:** It's probably worth while looking into a tool like [RVM](http://rvm.io/), [rbenv](http://rbenv.org) or similar that will let you create gemsets so that you don't pollute the system rubygems unnecessarily.

4. Now start up Jekyll and activate LSI (add `--watch` if you want to rebuild on any change to your content):

        $ jekyll serve --lsi

5. Make yourself a coffee with all the extra time you're going to save not sitting around waiting for the LSI indexer to finish!

Et voilà! Super speedy site rebuilds with more intelligent related posts for each page.


 *[LSI]: Latent Semantic Indexing
 *[GNU]: GNU's Not Unix!
 *[GSL]: GNU Scientific Library
 *[RVM]: Ruby Version Manager

  [brew]: http://brew.sh/
  [xcode]: https://itunes.apple.com/au/app/xcode/id497799835?mt=12
