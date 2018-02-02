---
layout: post
title: Persistence Registry keys and Windows Incident Response
date: '2010-10-21T14:25:00.000+02:00'
author: Xavier Garcia
tags:
- incident response
- registry
modified_time: '2010-10-21T14:25:47.713+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1628099332891288686
blogger_orig_url: http://www.shellguardians.com/2010/10/persistence-registry-keys-and-windows.html
---
The [Sans Computer Forensics](https://blogs.sans.org/computer-forensics/2010/10/20/digital-forensics-autorun-registry-keys/) blog discusses how to query certain registry keys to find secondary indicators of a compromise.  
  
[Dave Hull](https://blogs.sans.org/computer-forensics/author/trustedsignal/) has created a list of registry keys that can be used to run malware at boot time. He used [AutoRuns](http://technet.microsoft.com/en-us/sysinternals/bb963902.aspx) from [Microsoft Sysinternals](http://technet.microsoft.com/en-us/sysinternals/default.aspx) to pull the list of registry keys.  
  
The list of keys are available :  
  
  
[XPSP3_HKCU_Startup_Locations.txt](http://trustedsignal.com/IR/XPSP3_HKCU_Startup_Locations.txt) - cannot be remotely queried 
[XPSP3_HKLM_Startup_Locations.txt](http://trustedsignal.com/IR/XPSP3_HKLM_Startup_Locations.txt) - can be remotely queried
