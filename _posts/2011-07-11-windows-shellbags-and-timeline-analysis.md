---
layout: post
title: Windows Shellbags and Timeline Analysis
date: '2011-07-11T10:57:00.000+02:00'
author: Xavier Garcia
tags:
- forensics
- registry
- timeline
modified_time: '2011-07-11T10:57:17.420+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7752002713168542087
blogger_orig_url: http://www.shellguardians.com/2011/07/windows-shellbags-and-timeline-analysis.html
---
I have learned about the Windows Registry and the Shellbags, via this good [post](http://computer-forensics.sa
ns.org/blog/2011/07/05/shellbags) written [Chad Tilbury](http://computer-forensics.sans.org/blog/au
thor/ctilbury "View all posts by Chad Tilbury") on the [Sans Computer Forensics](http://computer
-forensics.sans.org/blog/2011/07/05/shellbags) blog.  
  
These registry keys store the preferences of each folder that has been opened **at least one time** with Windows Explorer (local, remote, portable devices, etc.). Thus, the simple existence of these entries and the given timestamps indicates that the intruder accessed the resources, being useful as another source of information to perform our timeline analysis.  
  
The [article](http://computer-forensics.sans.org/blog/2011/07/05/shellbags) explains that there are some differences between Windows XP and Windows 7 and the author recommends the tool ca lled [Sbag](http://www.tzworks.net/prototype_page.php?proto_id=14) from TZworks.
