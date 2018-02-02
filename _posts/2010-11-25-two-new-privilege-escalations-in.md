---
layout: post
title: Two new privilege escalations in Windows
date: '2010-11-25T09:14:00.001+01:00'
author: Xavier Garcia
tags:
- escalation
- windows
- privilege
modified_time: '2010-11-25T09:25:32.831+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4496603230331190418
blogger_orig_url: http://www.shellguardians.com/2010/11/two-new-privilege-escalations-in.html
---
Two new privilege escalations in Windows have appeared this week.  
  
Privilege escalation in the Scheduler
=====================================
Via [h-online.com](http://www.h-online.com/security/news/item/Exploit-released-for-unpatched-Stuxnet-hole-1140196.html)  

> Microsoft has already [patched](http://www.h-online.com/news/item/Microsoft-Patch-Tuesday-One-Stuxnet-hole-remains-open-1106886.html) three of the four security holes exploited by [Stuxnet](http://www.h-online.com/news/item/Stuxnet-brings-more-new-tricks-to-cyberwar-1098810.html), but the fourth hole remains unpatched. Now, an [exploit](http://www.exploit-db.com/exploits/15589/), currently being circulated on the web, exploits the remaining hole in the Windows Task Planner to access protected system directories – even if a user is only logged in with limited access privileges. Experts call this a [privilege escalation attack](http://en.wikipedia.org/wiki/Privilege_escalation).

> According to webDEViL, who developed the exploit, the demo malware works under Windows 7, Vista and Server 2008, both in their 32-bit and in the 64-bit versions.

  
Privilege escalation in the Registry
====================================
Via [isc.sans.edu](http://isc.sans.edu/diary.html?storyid=9988&rss)  [exploit-db.com](http://www.exploit-db.com/sploits/uacpoc.zip)  [packetstormsecurity.org](http://packetstormsecurity.org/files/view/96091/uacpoc.zip)  

> Today proof of concept code (source code, with a compiled binary) of a 0-day privilege escalation vulnerability in almost all Windows operating system versions (Windows XP, Vista, 7, Server 2008 ...) has been posted on a popular programming web site.

> The vulnerability is a buffer overflow in kernel (win32k.sys) and, due to its nature allows an attacker to bypass User Access Control (UAC) on Windows Vista and 7 operating systems.  
> What’s interesting is that the vulnerability exist in a function that queries the registry so in order to exploit this the attacker has to be able to create a special (malicious) registry key. Author of the PoC managed to find such a key that can be created by a normal user on Windows Vista and 7 (so, a user that does not even have any administrative privileges).

> The PoC code creates such a registry key and calls another library which tries to read the key and during that process it ends up calling the vulnerable code in win32k.sys. Since this is a critical area of the operating system (the kernel allows no mistakes), the published PoC only works on certain kernel versions while on others it can cause a nice BSOD. That being said, the code can be probably relatively easily modified to work on other kernel versions.
