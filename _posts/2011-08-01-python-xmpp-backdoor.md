---
layout: post
title: Python XMPP backdoor
date: '2011-08-01T19:02:00.003+02:00'
author: Xavier Garcia
tags:
- backdoor
- Python
- xmpp
modified_time: '2011-08-02T09:10:53.939+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2961209277494548515
blogger_orig_url: http://www.shellguardians.com/2011/08/python-xmpp-backdoor.html
---
Following the previous post, I thought it would be nice to find alternative ways to  code a backdoor  while using Python as the scripting language.

One of my first ideas was to write a simple backdoor that would use some kind of IM (Instant Messaging), like the script kiddies do with IRC. Yes, I can comfortably sit in front of my desk and wait until one of my XMPP bots pops-up in my list of on-line contacts!

I found some easy examples to construct a bot using the python-xmpp library and I reused most of the code.  Pretty script kiddie all together :)

The code can be found here: [xmppshell.py](http://ghosthunter.googlecode.com/svn/trunk/scripts/xmppshell/xmppshell.py)
