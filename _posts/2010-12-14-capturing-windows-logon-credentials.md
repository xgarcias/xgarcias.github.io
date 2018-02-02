---
layout: post
title: Capturing Windows Logon Credentials with Metasploit
date: '2010-12-14T08:35:00.000+01:00'
author: Xavier Garcia
tags:
- capture
- Metasploit
- credentials
- windows
modified_time: '2010-12-14T08:35:16.874+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8860983180646446057
blogger_orig_url: http://www.shellguardians.com/2010/12/capturing-windows-logon-credentials.html
---
Great [blog post](http://blog.metasploit.com/2010/12/capturing-windows-logons-with.html) from the [Metasploit blog](http://blog.metasploit.com/) that explains how to use a keylogger to capture the Windows Logon credentials.  
  
Smartlocker is a script meant to capture the Windows credentials used to unlock the session.  
  
Behavior:  
- Migrates to winlogon.exe  
- Waits for the session to be locked (the session is idle).  
- Starts the keylogger until the session is unlocked (by typing the username and the password)  
- Stops the keylogger  
- The credentials are stored in a text file located in **/home/{user}/.msf3/logs/scripts/smartlocker/**
