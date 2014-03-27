---
layout: post
title: Tips for mac-hosted virtual machines
tags:
  - Mac
  - Virtual Machines
date: 06 May 2007 18:30:00
---

So you’ve just finished downloading, installing and setting up a shiny new virtual machine using either [Parallels Desktop for Mac][1], or [VMware Fusion][2]. What’s that you say? Your machine is now really slow? It freezes for seconds at a time?

Well, that’s to be expected - you are effectively running two operating systems on your mac now. Keep that statement in mind, because my tips can’t do anything about that. **Your machine will be slower whilst running a virtual machine**. Don’t despair - we should be able to make things a little more responsive.

I look after a Mac Pro, an iMac and a MacBook Pro that have all been running Windows-based virtual machines for the past year without major issue - along the way, I’ve found a few tips that have made the virtual machines and my macs run a lot faster than they otherwise would have.

I’ll cover off three things below:

*   General tips for making your virtual machines faster;
*   Tips for [Parallels Desktop for Mac][1];
*   Tips for [VMware Fusion][2];

#### General tips for making your virtual machines faster

1.  **Buy as much RAM as you can afford**. Seriously - more RAM means that your virtual machines won’t have to page out to disk as much, your mac will remain more responsive and your life will generally be much happier (OK, perhaps that last bit is going too far) - obviously CPU speed is important too, but you won’t see anywhere near the same improvement as just adding more RAM;
2.  **The main speed decrease you’ll see when running a virtual machine comes from disk throughput**. Your hard disk will churn and thrash much more than it does when you’re just running Mac OS X on its own - but you can do a couple of things to help that:
    *   Dynamically expanding disks are good in most circumstances - especially for users without huge amount of disk space, but they shouldn’t be used in any situation where disk speed is essential. Each time the dynamically expanding disk reaches it’s bounds (the size of the space it has allocated itself), it needs to allocate more space which will cause the virtual machine to pause slightly;
    *   If you intend to host a server, or run applications that will cause either operating system to use more virtual memory, my experience has been that creating a separate, statically allocated virtual disk (a disk that doesn’t dynamically expand) and moving your guest operating system’s swap or pagefile to that. I generally make mine 5Gb in size, and tell my windows guests to create a pagefile between 1024 - 4096 Mb - this means your disk will thrash a little when you first start your virtual machine, but once it’s running you’ll find things to be smoother;
    *   Always, always, always run your virtual machines off a separate disk if you have a slower drive in your mac. My MacBook Pro is much more responsive on the mac side when it doesn’t need to compete with an entire other operating system sucking up it’s hard disk cycles. I run my virtual machines off of firewire disks, as firewire is generally much faster that USB 2.0 for purposes such as this;
3.  **Visit the forums for your product**. For Parallels Desktop for Mac, the address is [http://forum.parallels.com/](). For VMware Fusion, the address is [http://communities.vmware.com/community/vmtn/desktop/fusion]();

#### Tips for Parallels Desktop for Mac

1.  In general, Parallels Desktop’s default setting are pretty good already - you shouldn’t need to change them too much;
2.  Ensure that your Virtual Machine’s cache policy is set to “**Mac OS X**” on slower disks (you can find this in your virtual machine’s settings under “*Options > Advanced > Cache policy*”. Setting it to “**Virtual machine**” over “**Mac OS X**” will mean that your guest operating systems get priority access to your hard disks. Given that the guests will only ever be as fast as your mac can go, I personally find no use for the “**Virtual machine**” option;
3.  If you don’t need sound, remove the sound device (or at least set the sound input device to null) - there seems to be slow down when this is enabled (I’m not sure whether it is a bug - I’ll update this post when I know);

#### Tips for VMware Fusion

1.  **Always use the latest version of Fusion available**. Fusion’s performance has gotten much, much better since the beta, and the 1.1 release screams;
2.  **Always use SCSI disks with Fusion** - IDE disks are (at this stage) much, much slower than their SCSI counterparts. Windows XP doesn’t support SCSI disks out of the box, so please be sure to use Fusion’s easy installer - this will set-up your Windows-based virtual machines to use SCSI disks without any mucking around;
3.  Unless you have a multi-CPU Mac Pro monster, allowing your virtual machines to virtualise more than one CPU will just slow things down. **That means you Core Duo and Core 2 Duo users - it sounds cool to have 2 CPUs under your guest, but you’ll get better performance without them**;
4.  Generally speaking, modifying your graphics settings in Fusion don’t impact performance - if you need Direct X 8 compatibility, turn it on. If you don’t - well, it doesn’t really seem to do anything to performance, so you might as well leave it off until you need it;

 [1]: http://www.parallels.com/en/products/desktop/
 [2]: http://vmware.com/mac/
