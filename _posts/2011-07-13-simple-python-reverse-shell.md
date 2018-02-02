---
layout: post
title: Simple Python reverse shell
date: '2011-07-13T18:47:00.000+02:00'
author: Xavier Garcia
tags:
- reverse shell
- Python
modified_time: '2011-07-13T18:47:04.072+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4818285081540259603
blogger_orig_url: http://www.shellguardians.com/2011/07/simple-python-reverse-shell.html
---
Some days ago, [Rel1k](http://www.secmaniac.com/) published a [post](http://www.secmaniac.com/june-2011/creating-a-13-line-backdoor-worry-free-of-av/) explaining that he decided to include a small Pytho n backdoor in [SET](http://www.secmaniac.com/download/).

I gave it a try but I found some problems when executing the script in Linux.

* The '**quit**' command should let the backdoor close the connection and finish its execution, but it was not working.  The string '**quit\n'** is received  and the backdoor sends it to the shell instead of quitting.
* When Control+C is pressed,  ; the netcat listener finishes the execution and this leaves the backdoor hanging in an infinite loop, consuming lots of resources (while(True){} without any sleep).

I have made a few changes in the script to solve the problems I found and it also connects back again in case we have pressed Control+C by mistake, so we do not lose our shell :)

The modified version can be found here: [python_reverse_shell.py](http://ghosthunter.googlecode.com/svn/trunk/metasploit/shell/python_reverse_shell.py)  
