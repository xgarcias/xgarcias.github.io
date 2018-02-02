---
layout: post
title: Nessus scan through a socks Meterpreter pivot
date: '2010-10-25T11:04:00.002+02:00'
author: Xavier Garcia
tags:
- pivot
- socks
- meterpreter
- nessus
modified_time: '2010-11-01T19:58:55.622+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5259475749764141206
blogger_orig_url: http://www.shellguardians.com/2010/10/nessus-scan-through-socks-meterpreter.html
---
Great [article](http://www.digininja.org/blog/nessus_over_sock4a_over_msf.php) from [digininja.org](http://www.digininja.org/blog) that explains how to scan a target network with Nessus through a Meterpreter session.  
  
It is achieved by setting up a pivot and using the **auxiliary/server/socks4** module. Since the Nessus server does not natively support socks, we have to use a wrapper like proxychains or socksify, as explained in the article.
