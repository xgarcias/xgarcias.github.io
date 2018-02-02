---
layout: post
title: Anatomy of the RSA compromise
date: '2011-04-11T11:19:00.000+02:00'
author: Xavier Garcia
tags:
- zero-day
- flash
- RSA
- social engineering
- comproise
modified_time: '2011-04-11T11:19:13.479+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2386667725778866998
blogger_orig_url: http://www.shellguardians.com/2011/04/anatomy-of-rsa-compromise.html
---
This [blog post](http://blogs.rsa.com/rivner/anatomy-of-an-attack/) from the RSA explains how the attackers gained access to their data.

In a nutshell, the attackers used social engineering to let an employee open an Excel Spreadsheet that contained a Flash object  ( zero-day CVE-2011-0609). Once they back-doored the computer, they used the credentials to gain further access on the network (privileged accounts and systems) and they stole the data.
