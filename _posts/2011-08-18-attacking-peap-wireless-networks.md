---
layout: post
title: Attacking PEAP wireless networks
date: '2011-08-18T11:38:00.002+02:00'
author: Xavier Garcia
tags:
- security
- brute-force
- attack
- wireless
modified_time: '2011-08-18T11:40:40.496+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7918322427004015594
blogger_orig_url: http://www.shellguardians.com/2011/08/attacking-peap-wireless-networks.html
---
Great [video](http://www.securitytube.net/video/2039), as always, posted by Vivek Ramachandran on [SecurityTube](http://www.securitytube.net/).

This time, Vivek explains how to attack PEAP networks.  In a short resume, a Honeypot is setup with a roge AP and a Radius server in order to get the challenge and response  (802.1X) sent when a unaware user connects to our system.

Once we have captured the challenge and the response sent to our own Radius server, we can use the tool called [asleap](http://www.willhackforsushi.com/Asleap.html), written by Joshua Wright, that will brute-force the password with a dictionary attack.

<iframe frameborder="0" height="320" src="http://player.vimeo.com/video/26365581?title=0&amp;byline=0&amp;portrait=0" width="400"></iframe>

[WLAN Security Megaprimer 33](http://vimeo.com/26365581) from [Vivek Ramachandran](http://vimeo.com/user2264240) on [Vimeo](http://vimeo.com/).
