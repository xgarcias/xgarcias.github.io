---
layout: post
title: Fetching the SAM and System Files Without Shutting Down Windows
date: '2011-11-11T10:03:00.000+01:00'
author: Xavier Garcia
tags:
- pentest
- shadow copies
- windows
modified_time: '2011-11-11T10:03:17.230+01:00'
thumbnail: https://i.ytimg.com/vi/ant3ir9cRME/default.jpg
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2480132959514371452
blogger_orig_url: http://www.shellguardians.com/2011/11/fetching-sam-and-system-files-without.html
---
Via [securitybydefault](http://www.securitybydefault.com/2011/11/obtencion-del-fichero-sam-y-system-sin.html) [Spanish]

The linked blog post explains how to fetch the SAM and System files from a Windows computer without shutting down the system.

Since both files are locked by other processes, they cannot be read. Therefore, the standard procedure would be shutting down Windows and running a live distribution to obtain a copy.

The article points to a [talk given by Tim Tomes and Mark Bagget](http://www.irongeek.com/i.php?page=videos/hack3rcon2/tim-tomes-and-mark-baggett-lurking-in-the-shadows) in [Hack3rcon II](http://hack3rcon.org/), where they introduce a script they wrote to extract the files  by creating [Shadow Copies](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx).

<iframe allowfullscreen="" frameborder="0" height="315" src="http://www.youtube.com/embed/ant3ir9cRME" width="560"></iframe>
