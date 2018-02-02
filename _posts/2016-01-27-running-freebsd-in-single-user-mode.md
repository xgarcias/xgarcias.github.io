---
layout: post
title: Running FreeBSD in single user mode with zfs on root
date: '2016-01-27T17:58:00.002+01:00'
author: Xavier Garcia
tags:
- user
- zfs
- root
- single
- freebsd
modified_time: '2016-01-27T17:59:46.632+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4816986008450364145
blogger_orig_url: http://www.shellguardians.com/2016/01/running-freebsd-in-single-user-mode.html
---
Today I bricked a server (long story, etc ...) and I had to fix it in single user mode. The process is very simple.

* Use the boot loader to enter in single user mode
* Press Intro to run /bin/sh
* mount all the zfs volumes:
  ```shell
  $ zfs mount -a
  ```
* Mount the ROOT volume read-write:
  ```shell
  $ zfs set readonly=off zroot/ROOT/default
  ```
* Fix what you broke
* Reboot the server
