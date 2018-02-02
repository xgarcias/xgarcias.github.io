---
layout: post
title: EAP-MD5 Offline password attacks
date: '2011-04-27T11:26:00.001+02:00'
author: Xavier Garcia
tags:
- 802.1x
- eap-md5
- offline attack
modified_time: '2011-04-27T11:26:33.412+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6843729277527805093
blogger_orig_url: http://www.shellguardians.com/2011/04/eap-md5-offline-password-attacks.html
---
This [post](http://pauldotcom.com/2011/04/eap-md5-offline-password-attac.html) from [Pauldotcom](http://pauldotcom.com/) explains how to perform dictionary offline attacks against EAP-MD5 (802.1X protected networks)  authentication packets.

Once we have a packet capture with the authentication packets, the post offers two possibilities:
* Patched version of [xtest](http://xtest.sourceforge.net/) to read the passwords through a pipe (John the Ripper produces the password list)
* A small Scapy script  called  [eapmd5crack.py](http://lanmaster53.com/wp-content/uploads/tools/eapmd5crack.py)
