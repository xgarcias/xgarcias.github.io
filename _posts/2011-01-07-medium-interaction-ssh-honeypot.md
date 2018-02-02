---
layout: post
title: Medium interaction SSH honeypot
date: '2011-01-07T09:39:00.000+01:00'
author: Xavier Garcia
tags:
- ssh
- script kiddies
- honeypot
modified_time: '2011-01-07T09:39:39.826+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2649651339769415252
blogger_orig_url: http://www.shellguardians.com/2011/01/medium-interaction-ssh-honeypot.html
---
Thanks to a tweet made by [HD Moore](http://twitter.com/hdmoore/)  I found  a hilarious  website called [iwatchedyourhack.org](http://iwatchedyourhack.org/)  that posts transcripts of script kiddies attacking honeypots. :)

I guess many people is using SSH honeypots like [kippo](http://code.google.com/p/kippo/).

> Kippo is a medium interaction SSH honeypot designed to log brute force attacks and, most importantly, the entire shell interaction performed by the attacker.

>  some interesting features:

> * Fake filesystem with the ability to add/remove files. A full fake filesystem resembling a Debian 5.0 installation is included
> 
> * Possibility of adding fake file contents so the attacker can 'cat' files such as /etc/passwd. Only minimal file contents are included
> 
> * Session logs stored in an [UML compatible](http://user-mode-linux.sourceforge.net/) format for easy replay with original timings
> 
> * Just like Kojoney, Kippo saves files downloaded with wget for later inspection
> 
> * Trickery; ssh pretends to connect somewhere, exit doesn't really exit, etc
