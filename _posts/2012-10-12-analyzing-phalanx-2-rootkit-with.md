---
layout: post
title: 'Analyzing  the Phalanx 2 Rootkit with Volatility '
date: '2012-10-12T15:32:00.000+02:00'
author: Xavier Garcia
tags:
- Linux
- forensics
- volatility
- rookit
modified_time: '2012-10-12T15:32:10.705+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5209136317163713023
blogger_orig_url: http://www.shellguardians.com/2012/10/analyzing-phalanx-2-rootkit-with.html
---
[Andrew Case](https://twitter.com/attrc) has written a [great blog](http://volatility-labs.blogspot.de/2012/10/phalanx-2-revealed-using-volatility-to.html) post in which he analyzes  the Linux rootkit Phalanx2 with [Volatility](http://code.google.com/p/volatility/).

He explains all the common steps:
* Dump the memory with [lime](http://code.google.com/p/lime-forensics/).
* List hidden processes.
* File descriptors opened by the hidden process ( open sockets!).
* Network connections.
* Hooked system callas
* Recover

At the end of the post, Andre Case makes a complete forensic analysis of the kernel modules and the binaries used to inject the rootkit.
