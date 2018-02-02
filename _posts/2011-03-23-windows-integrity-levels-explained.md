---
layout: post
title: Windows Integrity Levels explained
date: '2011-03-23T13:56:00.004+01:00'
author: Xavier Garcia
tags:
- windows
- integrity levels
modified_time: '2011-03-23T15:01:11.177+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8075294391613705925
blogger_orig_url: http://www.shellguardians.com/2011/03/windows-integrity-levels-explained.html
---
This [post](http://isc.sans.edu/diary.html?storyid=10531) from the [Internet Storm Center](http://isc.sans.edu/) explains the  concept of the Integrity Levels, that is a tool available  on Windows Vista, 7 and 2008.  
  

> Integrity levels can restrict one process from interacting with another process even if both processes are running under the same user account and even if the user has administrative privileges.

  
Basically,  a process running under a lower integrity level will be limited in the way it can interact with process that run in a higher integrity level, regardless the access rights. This can be really helpful to mitigate a possible exploitation.  
  

> This is why it's advantageous to run the processes that are likely to be targeted by exploits under the Low integrity level. For instance, if a browser running under the Low integrity level gets exploited, the attacker's payload will have a hard time injecting itself into the majority of other processes or modifying critical files.

  
It seems it is a key tool used to create sandboxes in  Internet Explorer,  Chrome and the new Adobe Acrobat.  
  
The article links to the following blog post written by Didier Stevens and called [Integrity Levels and DLL Injection](http://blog.didierstevens.com/2010/09/07/integrity-levels-and-dll-injection/). It describes how this feature blocks a DLL injection attempt from a Low Integrity process to another with Medium Integrity.
