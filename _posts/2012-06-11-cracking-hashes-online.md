---
layout: post
title: Cracking Hashes Online
date: '2012-06-11T10:05:00.000+02:00'
author: Xavier Garcia
tags:
- pentest
- cracking
- credentials
- hash
modified_time: '2012-06-11T10:05:25.102+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3229069923024922154
blogger_orig_url: http://www.shellguardians.com/2012/06/cracking-hashes-online.html
---
Perhaps this tool is well known within the community, but I was not aware of it until now. [findmyhash](http://code.google.com/p/findmyhash/) is a Python script that searches for hashes in different online services, supporting the most common ones: MD5, SHA1, LM, NTLM, etc. (check the website for more details).
 
Looking at the [source code](http://code.google.com/p/findmyhash/source/browse/trunk/findmyhash.py), it uses many  websites I was not aware of.

It is kinda neat that you may not need to use brute force to crack a hash, but the downside ,of course, is that you are sending your hashes to services you may not trust 100%.  Would it be legit to use it during a pentest since we are sending data from our costumers to third party services?
