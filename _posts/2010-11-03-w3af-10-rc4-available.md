---
layout: post
title: w3af 1.0-rc4 available
date: '2010-11-03T11:41:00.000+01:00'
author: Xavier Garcia
tags:
- w3af
modified_time: '2010-11-03T11:41:26.328+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1962192777106454346
blogger_orig_url: http://www.shellguardians.com/2010/11/w3af-10-rc4-available.html
---
[Andres Riancho](http://www.bonsai-sec.com/es/about-us/founder.php) has [announced](http://lists.grok.org.uk/pipermail/full-disclosure/2010-November/077246.html)  that a new version of w3af is available.  
  

> Just to name a few things we've done for this release:
> * We've written new HOWTO documents for our users
> * Considerably improved the speed of all grep plugins
> * Replaced Beautiful Soup by the faster libxml2 library
> * Introduced the usage of XPATH queries that will allow us to improve performance and reduce false positives
> * Fixed hundreds of bugs
>
> On this release you'll also find that after exploiting a vulnerability youcan leverage that access using our Web Application Payloads, a feature that we developed together with Lucas Apa from Bonsai Information Security. These payloads allow you to escalate privileges and will help you get from a low privileged vulnerability (e.g. local file read) to a remote code execution. In order to try them, exploit a vulnerability, get any type of shell and then run any of the following commands: help, lsp, payload tcp (the last one will show you the open connections in the remote box).
