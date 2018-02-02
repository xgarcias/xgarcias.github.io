---
layout: post
title: LUKS encrypted disk forensics
date: '2010-10-07T10:53:00.001+02:00'
author: Xavier Garcia
tags:
- forensics
- luks
- lvm
modified_time: '2010-10-07T10:53:36.984+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3833964379645882820
blogger_orig_url: http://www.shellguardians.com/2010/10/luks-encrypted-disk-forensics.html
---
This great [article](https://blogs.sans.org/computer-forensics/2010/10/06/images-dmcrypt-lvm2/) from [Sans Computer Forensics](https://blogs.sans.org/computer-forensics/)  shows how to perform forensics investigations in a disk image that contains [LUKS](http://en.wikipedia.org/wiki/LUKS) volumes.  
  
The following tricks appear in the article:  

*   Use **losetup** to create a read-only logical device pointing to the LUKS partition.
*   Use **cryptsetup** to verify that the partitions is LUKS and then mount it.
*   LVM2 Fu to load/unload the Volum Groups
