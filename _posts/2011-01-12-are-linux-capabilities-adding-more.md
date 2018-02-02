---
layout: post
title: Are the Linux capabilities adding more security?
date: '2011-01-12T13:33:00.003+01:00'
author: Xavier Garcia
tags:
- Linux
- root
- capabilities
modified_time: '2011-01-12T14:10:22.935+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1817336701424701751
blogger_orig_url: http://www.shellguardians.com/2011/01/are-linux-capabilities-adding-more.html
---
Many Linux distributions are moving towards [Capabilities](http://www.ibm.com/developerworks/library/l-posixcap.html) in order to get rid of SUID/SGID binaries.  Yes, it sounds nice because it splits the powers into smaller privileges and also adds a high level of granularity.  
  
In practice, it depends how the capabilities are implemented and what privilege gives each capability, because there are cases where the program ends up with insane privileges. Of course, this can cause some troubles  and we will see many problems (exploits?) in the future.  
  
The following [article](http://www.h-online.com/security/news/item/Expert-Linux-capabilities-don-t-add-security-1164658.html) explains some of the cases discussed during the past weeks, that led to local root privilege escalation. They point to the following [exploit](http://lists.grok.org.uk/pipermail/full-disclosure/2011-January/078350.html) released in the Full disclosure mailing list and also the post [sent](http://forums.grsecurity.net/viewtopic.php?f=7&t=2522) by Spender to the [Grsecurity Forum](http://forums.grsecurity.net/), that is a good reading.
