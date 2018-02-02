---
layout: post
title: Presentation about botnets in SIGINT'10, Koln
date: '2010-10-20T11:48:00.004+02:00'
author: Xavier Garcia
tags:
- storm
- sigint
- waledac
- videos
- botnets
modified_time: '2010-11-01T20:08:38.904+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5588881079369993249
blogger_orig_url: http://www.shellguardians.com/2010/10/presentation-about-botnets-in-sigint10.html
---
[SIGINT'10](http://events.ccc.de/sigint/2010/wiki/Willkommen) took place between the 22nd and the 24th of May in Koln, Germany. The videos are also available and [hosted](http://ftp.ccc.de/events/sigint10/video/) by [ccc](http://www.ccc.de/).  
  
I just saw the presentation made by Thorsten Holz and called '_Botnets in 2010 - Status Quo and Future Threats'_.  
  
As a quick resume, it does a quick introduction to the botnets and its arquitecture and then talks about Storm Worm and Waledac.  
  
**Storm Worm**  

*   Not centralized C & C thanks to p2p
*   Fast flux domains
*   Uses infected computers with public IP addresses to proxy the content back to the backend: spam pages or with exploit packs. It is hard to track  and offers high availability.
*   The nated machines are user to send spam and dos attacks.
*   Template based spamming. The template is sent to the bots that then send the spam.
*   Mitigation: join the network and disrupt the communication channel between the bots (Stormfucker in 25c3 CCC)

**Waledac**

*   Successor of Storm Worm and perhaps created by the same group
*   Uses HTTP to tunnel trafic (major change) between the nated machines and the repeaters
*   multi-tier architecture ('hybrid' p2p), like storm worm
*   Static backend servers that host the content
*   Fast flux domains for C&C
*   Template based spamming.
*   The mitigation effort was called 'Operation b49' and took down the botnet in February 2010.

  
  
  
The video can be found [here](http://ftp.ccc.de/events/sigint10/video/sigint10_3891_en_botnets_in_2010.mkv).
