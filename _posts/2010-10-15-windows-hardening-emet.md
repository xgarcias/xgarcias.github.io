---
layout: post
title: 'Windows hardening: EMET'
date: '2010-10-15T16:40:00.000+02:00'
author: Xavier Garcia
tags:
- hardening
- windows
- EMET
modified_time: '2010-10-15T16:40:41.784+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8969576654983951817
blogger_orig_url: http://www.shellguardians.com/2010/10/windows-hardening-emet.html
---
[EMET](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=c6f0a6ee-05ac-4eb6-acd0-362559fd2f04) (Microsoft's Enhanced Mitigation Experience Toolkit) is a tool that enables the security features that are not enabled by default on the applications. Unfortunately, Windows leaves the applications choose which security features should be enabled by setting specific flags, so many attacks can succeed  even though the security protections are enabled in the operative system.  
  
In a nutshell, EMET is a DLL that permits to enable the security features in runtime, for applications that were compiled without it, like DEP (Data Execution Prevention) and ASLR (Address Layout Space Randomization).  
  
You can find more information about this tool as well as examples in this [article](http://www.h-online.com/security/features/Damage-limitation-Mitigating-exploits-with-Microsoft-s-EMET-1102501.html) from [H Security](http://www.h-online.com/).
