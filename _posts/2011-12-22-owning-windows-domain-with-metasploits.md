---
layout: post
title: Owning a Windows Domain with Metasploit's Incognito and Persistence Modules
date: '2011-12-22T16:58:00.000+01:00'
author: Xavier Garcia
tags:
- Metasploit
- compromise
modified_time: '2011-12-22T16:58:05.332+01:00'
thumbnail: https://i.ytimg.com/vi/7BYP8l1tlak/default.jpg
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2144607168765617086
blogger_orig_url: http://www.shellguardians.com/2011/12/owning-windows-domain-with-metasploits.html
---
Found via [@armitagehacker](http://twitter.com/armitagehacker) on Twitter.  
  
This video shows a demo that uses [Armitage](http://www.fastandeasyhacking.com/) ([Metasploit](http://metasploit.com/) to compromise a Windows Domain Controler.  
  
The attacker gains access to an unpatched Windows web server  by exploiting the classic MS08-067. On the web server, the attacker is able to [obtain the cached domain credentials](http://www.offensive-security.com/metasploit-unleashed/Fun_With_Incognito) of an administrator  and use them to compromise the domain controller.  
  
The attacker also makes use of the [persistence module](http://www.offensive-security.com/metasploit-unleashed/Persistent_Meterpreter_Service) to keep a foothold on the compromised system.

<iframe allowfullscreen="" frameborder="0" height="415" src="http://www.youtube.com/embed/7BYP8l1tlak" width="520"></iframe>
