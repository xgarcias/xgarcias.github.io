---
layout: post
title: Recovering Memory Filesystems With Volatility
date: '2012-08-20T16:33:00.002+02:00'
author: Xavier Garcia
tags:
- Linux
- forensics
- volatility
modified_time: '2012-08-20T16:35:47.784+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3921481431832932065
blogger_orig_url: http://www.shellguardians.com/2012/08/recovering-memory-filesystems-with.html
---
Via [memoryforensics.blogspot.de](http://memoryforensics.blogspot.de/2012/08/recoving-tmpfs-from-memory-with.html) ,  I have learned about a Volatility [plugin](http://code.google.com/p/volatility/source/browse/branches/linux-trunk/volatility/plugins/linux/tmpfs.py) that can list and extract _**tmpfs**_  filesystems from Linux memory images.

As the author of the blog post comments, many distributions are using this filesystem for different tasks (e.g. /tmp /dev/shm) with the benefit of not having to delete files  and also the added performance compared with traditional filesystems that are stored in hard drives.

Of course, this has some implications when performing a forensic analysis, because all the information contained will be lost if the investigator only make a disk image.  On top of this, /tmp and /dev/shm are one of the few directories that are world writable and, therefore, preferred by the attackers to store information.
