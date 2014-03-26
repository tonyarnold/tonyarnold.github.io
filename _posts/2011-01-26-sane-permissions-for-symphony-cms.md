---
publish: false
layout: post
title: "Sane permissions for Symphony CMS"
tags:  [Web Development]
date: 26 January 2011 14:46:00
---

I use [Symphony CMS](http://symphony-cms.com/) for almost all of my sites, and for my client sites as well. Here are a few tips I've found help to make your sites more secure, and ease development.

There are a few simple things I change on my sites that you should probably think about:

## Set sane permissions

If you're unfamiliar with how permissions work on UNIX, here's an oversimplified breakdown:

 * **Read** — means that the file or directory (and it's attributes) can be read. On a directory, this does not grant permission to read the contents of the directory (ie. the list of files inside the directory);
 * **Write** — means that you can make changes to the file or directory;
 * **Execute** — for directories, the execute permission allows the contents of the directory to be read (ie. list the files inside the directory). For files, this means that the file can be run as a executable process on your computer/server — this is almost **never** what you want.

The default [Symphony][1] install uses a permission mask of `775` for both directories and files created within the `workspace` directory. A permissions mask is composed of three discrete parts:

 1. The first number represents the **owner of the file**;
 2. The second number represents the **group of the file**;
 3. The third number represents **everyone else** ('other').

So [Symphony's][1] default permissions of `775` for both directories and files means:

 * **Owner** — can read, write and execute both directories and files created by Symphony;
 * **Group** — can read, write and execute both directories and files created by Symphony;
 * **Everyone** — can read and execute both directories and files created by Symphony;

Depending on your web host, this default might actually stop your site from working entirely — at the least it's a pretty insecure mask to use out of the box. The absolute bottom line is that **on a public web site, you should never grant any permissions unless they are absolutely necessary**. 

The directory permissions are (in most cases) completely OK. But the file permissions are not OK at all — you do not under nearly any circumstances want files within your `workspace` to be executable — not even by you. Leaving files executable within this directory leaves you open to somebody gaining access to your install and uploading a script or binary executable - if you remove the executable bit from all uploaded files, there's little chance someone can use uploaded files to do anything malicious to your site.

### Bottom line

I always set my file permissions to be `664`, and my `775` for directories when setting up a new [Symphony][1] install. 

If you know that your site will be run as a discrete user on your server, you could even consider removing write privileges for group as well - this is as simple as `755` for groups, and `644` for users. This might interfere with local development (depending on how your local install is setup), so I generally don't change this.



  [1]: http://symphony-cms.com/