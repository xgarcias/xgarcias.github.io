---
layout: post
title: Windows ASLR and the False Sense of Security
date: '2011-07-08T10:57:00.003+02:00'
author: Xavier Garcia
tags:
- security
- fail
- aslr
modified_time: '2011-07-08T11:10:21.247+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4844871334887093168
blogger_orig_url: http://www.shellguardians.com/2011/07/windows-aslr-and-false-sense-of.html
---
Lately, I have read a lot about exploits bypassing the [ASLR](http://en.wikipedia.org/wiki/Address_space_layout_randomization) protection. In particular, this [post](http://www.scriptjunkie.us/2011/06/bypassing-dep-aslr-in-browser-exploits-with-mcafee-symantec/) from [scriptjunkie.us](http://www.scriptjunkie.us/) and this [one](https://www.corelan.be/index.php/2011/07/03/universal-depaslr-bypass-with-msvcr71-dll-and-mona-py) from [corelan.be](https://www.corelan.be/).

I believe [ASLR](http://en.wikipedia.org/wiki/Address_space_layout_randomization) is a really good protection in systems where **all the software is making use of it and there is no room for exceptions**, but it is not true for Windows. Since this feature is optional on this platform, it only takes somebody to load on your program a DLL that has [ASLR](http://en.wikipedia.org/wiki/Address_space_layout_randomization) disabled to bypass all the protections that were carefully planed.

We have seen these examples with Java, McAfee and Symantec and I am sure we will find many more in the future, since Microsoft will be  trapped  supporting old software for long time if not ever. The only option I see is the Operative System enforcing these protections at low level.
