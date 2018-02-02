---
layout: post
title: FreeBSD in the desktop, my personal experience
date: '2014-11-28T13:50:00.000+01:00'
author: Xavier Garcia
tags: 
modified_time: '2014-11-28T13:50:57.322+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2049122635432466156
blogger_orig_url: http://www.shellguardians.com/2014/11/freebsd-in-desktop-my-personal.html
---
It has been a few months since I started (again) to run FreeBSD in the desktop, this time at work. I guess, it is being time to explain how it feels.

First of all, it wasn't the first time I have used FreeBSD at all. It used to be my desktop back in the university times and I have been running it in servers for quite a while. Therefore, I didn't have to start from scratch and figure out how things work.

It is subjective, but I remember I didn't need lots of time to adapt to the new environment when I first used it. I ran Debian in the old days, when you needed a bit of knowledge to get things running, that helped a lot to understand the inner workings of any "Unix like" operative system. Basically, I only had to learn how the start-up system worked and what the port tree was. The rest was pretty much the same and the documentation in the BSD projects is awesome!

At work, I was running [xubuntu](http://xubuntu.org/) because [Xfce](http://www.xfce.org/) has always been my desktop environment of choice and Ubuntu was easy and quick to install (lazy admin is lazy). My priority was to get things done at work and I only wanted a desktop that _**just works**_. Since then, it has always been a love-hate relationship.

I am the kind of person that wants to control and understand what is running in his box. This mindset is what made the sysadmin that I am today and pisses me off when I feel I am running a black box. This is what caused me installing Linux in a Macbook after a few weeks and later deciding not buying another anymore. Also, this was one of the main points to move back to FreeBSD this year.

I remember the times I could count with one hand the processes running in a Linux box. Ten years later we have things like systemd, polkit, freedesktop, dbus, pulsaudio, etc.. and Linux is slowly becoming something similar to the Windows I ran away from (I know I am starting a flame war). In many cases, the best way to get an account fixed is wiping the account and starting clean.

With FreeBSD I feel again at home. I installed [Xfce](http://www.xfce.org/) on top of a minimal installation plus a couple of other packages, I can control what is running and the documentation is excellent, in case I have to troubleshoot a problem.

I had two disks mirrored win ZFS, but now I use only a single SSD disk also with ZFS. The performance is great and I didn't need to completely reinstall after the disk replacement because I sent all the existing ZFS volumes over the network to the new box. Hopefully, [btrfs](https://btrfs.wiki.kernel.org/) will offer similar functionalities in the future.

The only downside I have found so far is the flash support, that needs to run with Linux emulation via [nspluginwrapper](http://nspluginwrapper.org/), but the widespread use of HTM5 will fix this later. I also have found some NFS performance problems against a NetApp filer and I had to use _**oldnfs**_ instead but I need to investigate more.
