---
layout: post
title: ProFTPD preauth remote buffer overflow
date: '2010-11-03T09:05:00.001+01:00'
author: Xavier Garcia
tags:
- preauth
- telnet
- overflow
- proftpd
modified_time: '2010-11-07T21:04:49.509+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2452320311556795222
blogger_orig_url: http://www.shellguardians.com/2010/11/proftpd-preauth-remote-buffer-overflow.html
---
TippingPoint , under the  [zero day initiative](http://www.zerodayinitiative.com/), has published a [preauth remote overflow](http://bugs.proftpd.org/show_bug.cgi?id=3521) in ProFTPD.  
  

> This vulnerability allows remote attackers to execute arbitrary code on vulnerable installations of ProFTPD. Authentication is not required to exploit this vulnerability. 
>
> The flaw exists within the proftpd server component which listens by default on TCP port 21. When reading user input if a TELNET_IAC escape sequence is encountered the process miscalculates a buffer length counter value allowing a user controlled copy of data to a stack buffer. A remote attacker can exploit this vulnerability to execute arbitrary code under the context of the proftpd process.

  
Welcome back to the 90's! This smells like a  classic exploit :D  
  
UPDATE:  the [exploit](http://lists.grok.org.uk/pipermail/full-disclosure/2010-November/077281.html) has been published as well as the [advisory](http://www.zerodayinitiative.com/advisories/ZDI-10-229/) from Zero Day Initiative.
