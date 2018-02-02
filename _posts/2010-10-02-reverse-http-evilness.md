---
layout: post
title: Reverse HTTP evilness
date: '2010-10-02T14:34:00.000+02:00'
author: Xavier Garcia
tags:
- reverse http shell
- Tor
- backdoor
- Python
- unix
modified_time: '2010-10-02T21:18:29.717+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-838664288099662540
blogger_orig_url: http://www.shellguardians.com/2010/10/reverse-http-evilness.html
---
Some months ago I heard people talking about using Tor to anonymously scan your target network by using the SOCKS interface and sockifying tools like NMAP, etc. What amazed  me was the [Tor backdoor](http://carnal0wnage.attackresearch.com/node/376) that the guys of [Carnal Ownage](http://carnal0wnage.attackresearch.com/) created. Unfortunately, it is only meant for Windows environments because it is the main platform that pentesters are working with.  
  
I came up with the idea of making something (a crappy script in my case) that could be executed easily in a Unix environment. Basically, I borrowed some RSA and Blowfish code implemented in Python and I created a reverse http shell that encrypts all the traffic.  
  
  
This script also permits to upload and download  small files. Unfortunately, Python is too ineficient in this case. Forget about using this method to upload big files.
  
The most interesting part is that it can use a HTTP Tor proxy to connect to a hidden service, so you can run a reverse backdoor and the destination will not be identified. Of course, I coded this script for fun and it should only be used for educational puposes and to show how difficult is to defend a network (and easly to fly under the radar).  
  
  
The [code](http://code.google.com/p/ghosthunter/source/browse/trunk/fimap/plugins/#plugins/reversehttp/pytor) is not finished yet because I have been too busy since then, but it works :D  
  
I think it is a good way to teach people that they cannot relay on tools to defend their networks. They have to understand that they are going to be compromised soon or later and they have to desing their networks to identify the existing compromise and respond to the incident as quick as possible.
