---
layout: post
title: Encrypting your Dropbox Data with EncFS
date: '2011-06-10T09:38:00.000+02:00'
author: Xavier Garcia
tags:
- encryption
- dropbox
- encfs
modified_time: '2011-06-10T09:38:32.879+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4605904051274074864
blogger_orig_url: http://www.shellguardians.com/2011/06/encrypting-your-dropbox-data-with-encfs.html
---
I have found this [post](http://www.webupd8.org/2011/06/encrypt-your-private-dropbox-data-with.html) via [Mubix](http://twitter.com/mubix) . This a recurrent subject and I have seen many posts in the past.  
  
Since there is a total lack of security in [Dropb ox](http://www.dropbox.com/), many people have thought it would be a good idea to encrypt its content, so only the legit owner ca n access the data. The problem comes when many solutions encrypt complete volumes, forcing us to sync the comple te volume to dropbox over and over again, which is not handy at all.  
  
The advantage of [EncFS](http://www.arg0.net/encfs) is that it encrypts per file, making it really convenient for our purpose.
