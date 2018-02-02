---
layout: post
title: Bypassing  antivirus signatures
date: '2011-01-17T10:40:00.003+01:00'
author: Xavier Garcia
tags:
- evasion
- antivirus
modified_time: '2011-01-17T11:16:08.168+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3721471697504313263
blogger_orig_url: http://www.shellguardians.com/2011/01/bypassing-antivirus-signatures.html
---
Last weekend I read a nice conversation in the #metasploit IRC channel. A user wanted to know how to bypass antivirus signatures and somebody pointed out  to a presentation  made by the [Offensive-Security](http://www.offensive-security.com/) guys in [Schmoocon](http://www.shmoocon.org/), back in 2008.  
  
In a nutshell,  we have to patch the binary with a Hex editor.  The original binary will be 'Xored' to avoid the AV signatures and also a new routine will be added at end of the DATA section to decode the contents of the binary in run-time.  
  
You can find  a copy of the video [here](http://www.offensive-security.com/videos/shmoocon-presentation-2008-video/shmoocon-presentation-2008.mp4)
