---
layout: post
title: 'Windows EMET: Enforcing Code Execution Protections'
date: '2011-05-30T11:36:00.000+02:00'
author: Xavier Garcia
tags:
- dep
- windows
- EMET
- aslr
modified_time: '2011-05-30T11:36:58.211+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1689142790777270481
blogger_orig_url: http://www.shellguardians.com/2011/05/windows-emet-enforcing-code-execution.html
---
This is a good [post](http://www.darkoperator.com/blog/2011/4/29/microsoft-emet.html) from darkoperator that explains how to use [EMET](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=c6f0a6ee-05ac-4eb6-acd0-362559fd2f04) to enforce code executi on protections in windows binaries, like ASLR and DEP.

As explained in the post, the applic ations have to be compiled with the right flags in order to use these protections by default, but they can also be manually enabled with [EMET](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=c6f0a6ee-05ac-4eb6-acd0-362559fd2f04).
