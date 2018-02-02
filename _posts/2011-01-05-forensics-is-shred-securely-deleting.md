---
layout: post
title: 'forensics: is Shred securely deleting the files?'
date: '2011-01-05T11:12:00.006+01:00'
author: Xavier Garcia
tags:
- forensics
- wipe
- shred
modified_time: '2011-01-05T11:36:24.773+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5493482086487250579
blogger_orig_url: http://www.shellguardians.com/2011/01/forensics-is-shred-securely-deleting.html
---
This [article](http://computer-forensics.sans.org/blog/2010/12/07/digital-forensics-quick-note-shred) from the [SANS Computer Forensics Blog](http://computer-forensics.sans.org/blog) analyzes how the tool [shred](http://blog.commandlinekungfu.com/2009/05/episode-32-wiping-securely.html) behaves when wiping files from the file system.  
  
If fact, like any other 'userland' tool, shred opens the file/s by using  the available system calls. Therefore the application cannot access some metadata that remains in the file system.  
  

> In the Linux/Unix realm we have tools like [shred](http://blog.commandlinekungfu.com/2009/05/episode-32-wiping-securely.html) for securely overwriting files before deleting them in order to prevent recovery of the deleted file.  If your adversary is sufficiently advanced (or just not lazy), they can obviously use these tools to frustrate your forensic investigation.  Previously, I had thought that shred removed all traces of the file from disk.  But in the course of some other file system research I was doing, I've realized that there may be a few lingering artifacts.
>
>  If you look at the shred source code, it simply opens the file like any normal user process, jumps to the beginning of the file, and proceeds to overwrite the file from beginning to end.  As a normal user process, it has access to the data blocks that make up the file content, but not the indirect block metadata.  The file system drivers in the OS "hide" the indirect blocks from the shred program.  A program that wanted to clobber the indirect block data would have to have superuser privileges so that it could open the raw disk device and attack the necessary blocks directly.  Normal user space programs like shred aren't going to have this level of access.

  
The author of the post verifies the behavior with [Sleuthkit](http://sleuthkit.org/) . As expected, shred is not able to access  an indirect block that contains metadata  and it does not get deleted. This only can be achieved by opening the raw device and overwriting the needed blocks, that needs admin. privileges.  
  
**UPDATE:** the file can still be completely recovered from the journal with ext3grep,  if it was recently deleted. We can find some examples [in this site](http://www.xs4all.nl/~carlo17/howto/undelete_ext3.html).  

>  Every time a file is accessed, it's Access Time is changed, and it's inode is written to disk, along with 31 other inodes that reside in the same block. When that happens, a copy of that block is written to the journal. Therefore, if your partition isn't too large compared to your journal, and if you at least recently accessed the files you want to recover, you might be able to recover the block pointers from the journal.
