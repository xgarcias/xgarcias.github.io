---
layout: post
title: Extracting memory mapped files from memory dumps
date: '2011-02-16T14:01:00.000+01:00'
author: Xavier Garcia
tags:
- memory mapped files
- volatility
modified_time: '2011-02-16T14:01:08.883+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3495299663321823164
blogger_orig_url: http://www.shellguardians.com/2011/02/extracting-memory-mapped-files-from.html
---
[computer-forensics.sans.org](http://computer-forensics.sans.org/) explains how to extract [memory mapped files from memory dumps](http://computer-forensics.sans.org/blog/2011/02/01/digital-forensics-extracting-event-logs-memory-mapped-files-memory-dumps). This technique is useful when the files we want to investigate (like log files)  are not available in the HD, perhaps because they were deleted.  
  
They use Volatility to extract from the dump all the files opened by the  _**Event Log service.**_  
  
[Memory Mapped File](http://en.wikipedia.org/wiki/Memory-mapped_file) is:  

> is a segment of [virtual memory](http://en.wikipedia.org/wiki/Virtual_memory "Virtual memory") which has been assigned a direct byte-for-byte correlation with some portion of a file or file-like resource. This resource is typically a file that is physically present on-disk, but can also be a device, shared memory object, or other resource that the [operating system](http://en.wikipedia.org/wiki/Operating_system "Operating system") can reference through a [file descriptor](http://en.wikipedia.org/wiki/File_descriptor "File descriptor"). Once present, this correlation between the file and the memory space permits applications to treat the mapped portion as if it were [primary memory](http://en.wikipedia.org/wiki/Primary_memory "Primary memory").
>
> The primary benefit of memory mapping a file is increased I/O performance, especially when used on small files.\[[citation needed](http://en.wikipedia.org/wiki/Wikipedia:Citation_needed "Wikipedia:Citation needed")\] Accessing memory mapped files is faster than using direct read and write operations for two reasons. Firstly, a system call is orders of magnitude slower than a simple change to a program's local memory. Secondly, in most operating systems the memory region mapped actually is the kernel's [page cache](http://en.wikipedia.org/wiki/Page_cache "Page cache") (file cache), meaning that no copies need to be created in user space.
