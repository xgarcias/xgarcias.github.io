---
layout: post
title: Securing  the network  with OTP and Radius
date: '2011-01-03T09:09:00.000+01:00'
author: Xavier Garcia
tags:
- otp
- open source
- radius
modified_time: '2011-01-03T09:09:58.579+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1309161957429933436
blogger_orig_url: http://www.shellguardians.com/2011/01/securing-network-with-otp-and-radius.html
---
Nice presentation from [SecTor 2010](http://www.sector.ca/) that explains how to use OTP and Radius to secure the network.  
  
Radius can easily be integrated with PAM: SSH, sudo, su, openvpn, postgresql, ...
  
I like the solution they offer to allow the users remotely access their desktop. FreeNX is tunneled through SSH (user authentication via OTP)  and offers X, VNC, RDP, desktop sharing  and session shadowing.  
  
[Video](http://secdocs.lonerunners.net/documents/details/3231-securing-your-network-with-open-source-technologies-and-standard-protocols-tips--tricks)  [Slides](http://secdocs.lonerunners.net/documents/details/3230-securing-your-network-with-open-source-technologies-and-standard-protocols-tips--tricks)
