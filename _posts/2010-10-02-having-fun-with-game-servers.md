---
layout: post
title: Having fun with game servers
date: '2010-10-02T21:37:00.000+02:00'
author: Xavier Garcia
tags:
- monitor
- Enemy territory
- Python
- Android
modified_time: '2010-10-02T21:42:06.378+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7580524147906947845
blogger_orig_url: http://www.shellguardians.com/2010/10/having-fun-with-game-servers.html
---
Past week I was bored and I needed to do something to keep me busy. I thought it would be nice to write a simple script that monitors my favorite game servers (Wolfenstein: Enemy Territory), so I know which map is currently being played as well as the number of players.  
  
I wrote two scripts: the first one is the desktop version and the second one for my Android telephone.  It took me only some hours to finish, so it is not impressive but it was funny :D  
  
[The desktop version](http://code.google.com/p/ghosthunter/source/browse/trunk/kernwaffe_monitor/kernwaffe_monitor.py) uses libnotify to pop-up a window everytime a new map is being played. It displays the map name and the number of used slots for each server.  
[  
](http://www.blogger.com/goog_1536354567)  
[The Android version](http://code.google.com/p/ghosthunter/source/browse/trunk/kernwaffe_monitor/kernwaffe_android.py) does pretty much the same but alerts me, vibrating or with text to speech, when one of the servers is unreachable.
