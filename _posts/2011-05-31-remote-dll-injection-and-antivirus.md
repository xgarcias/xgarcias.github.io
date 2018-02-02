---
layout: post
title: Remote DLL injection and Antivirus Evasion
date: '2011-05-31T10:48:00.000+02:00'
author: Xavier Garcia
tags:
- sleep
- evasion
- antivirus
- meterpreter
modified_time: '2011-05-31T10:48:56.888+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2252539955896974293
blogger_orig_url: http://www.shellguardians.com/2011/05/remote-dll-injection-and-antivirus.html
---
Great post written by [Mubix](http://www.room362.com/blog/2011/5/30/remote-dll-injection-with-meterpreter.
html), that explains a really interesting technique to bypass an Antivirus running in a Windows h ost.  
  
Mubix points out to a [DLL writ ten by Didier Stevens](http://blog.didierstevens.com/2011/04/27/suspender-dll/) that will suspend a process and its threads after a delay.  The idea behind is sending the Antivirus process to sleep in order to avoid detection during the pentest.  
  
I understan d that the DLL must be uploaded to the host before it is loaded onto the memory process and,  perhaps, this can be used by the Antivirus to flag the DLL before we have a chance to load it. I wonder if this also can be d one by Meterpreter without writing to disk.
