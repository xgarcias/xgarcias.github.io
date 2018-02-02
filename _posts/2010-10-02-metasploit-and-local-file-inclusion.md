---
layout: post
title: Metasploit and local file inclusion
date: '2010-10-02T13:56:00.000+02:00'
author: Xavier Garcia
tags:
- Fimap
- Metasploit
- Python
- LFI
modified_time: '2010-10-02T13:58:31.011+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-717170672366340425
blogger_orig_url: http://www.shellguardians.com/2010/10/metasploit-and-local-file-inclusion.html
---
I am not a super skilled hacker (probably I am the opposite ), but one thing I have is the mindset. Whenever I read something interesting,  I want to go beyond and I keep thinking about it until I come up with something.

Long time ago I read about an interesting project called [FIMAP](http://code.google.com/p/fimap/) that is meant to exploit LFI (Local File Inclusions) in web servers, mainly PHP. 

I thought that would be nice to integrate it somehow with Metaspoit because it is the framework that many people is using nowadays. It took me some time to write a Python wrapper that creates/encodes payloads and communicates with Metasploit using XMLRPC.


As a result, we have a Fimap plugin that interacts with a running Metasploit console and pops up  a reverse shell, for Windows and Unix. I had to make some changes with their help because I am not a skilled programmer and I didn't know how to implement a plugin system. I think it was a great experience!

The original code in my [subversion](http://code.google.com/p/ghosthunter/source/browse/#svn/trunk/fimap/plugins/msf) repository.
