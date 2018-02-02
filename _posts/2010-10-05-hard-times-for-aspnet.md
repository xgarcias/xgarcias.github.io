---
layout: post
title: Hard times for ASP.NET
date: '2010-10-05T09:11:00.003+02:00'
author: Xavier Garcia
tags:
- asp.net
- vulnerability
- ms10-070
modified_time: '2010-10-05T09:18:10.501+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1966448062638832312
blogger_orig_url: http://www.shellguardians.com/2010/10/hard-times-for-aspnet.html
---
On September 28th  Microsoft published the bulletin [MS10-070](http://www.microsoft.com/technet/security/bulletin/MS10-070.mspx) that fixed a information disclosure in ASP.NET  ( the .NET framework).  

  

As [David Aitel](http://lists.immunitysec.com/pipermail/dailydave/2010-October/006206.html) pointed out,  
  

> It's your basic massive break-the-internet nightmare, that Microsoft has avoided for many years since Code Red and the rest of the big worms ran rampant on IIS. It's interesting that this time around it's not a buffer overflow.

  

  

Looks like some people is having lots of fun lately and many system administrators are going to have a hard time.

  

ISC also dedicated an [entry](http://isc.sans.edu/diary.html?storyid=9625) in the Diary.

> In Microsoft .NET Framework 3.5 Service Pack 1 and above, this vulnerability can be used by an attacker to retrieve the contents of any file within the ASP.NET application, including web.config"   and  "This vulnerability can also be used for data tampering, which, if successfully exploited, could be used to decrypt and tamper with the data encrypted by the server.

> According to the bulletin, MSFT are aware of "active attacks".

  
If this is not enough,  Packet Storm Security published a [proof  of concept](http://packetstormsecurity.org/filedesc/Web.config_bruter.zip.html)  that exploits this vulnerability.  
  

>  Proof of concept exploit that demonstrates the downloading of Web.config. This affects unpatched versions of .NET framework 3.5 Sp1. Full details are available on the homepage.
