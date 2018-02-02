---
layout: post
title: Detecting time stamp manipulations in the file system
date: '2010-11-03T10:16:00.001+01:00'
author: Xavier Garcia
tags:
- forensics
- standard_information
- file_name
- ntfs
- time stamp
modified_time: '2010-11-03T10:16:31.984+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4874934748859160909
blogger_orig_url: http://www.shellguardians.com/2010/11/detecting-time-stamp-manipulation-in.html
---
Awesome article from [SANS computer forensics blog](https://blogs.sans.org/computer-forensics/) entitled [Digital Forensics: Detecting time stamp manipulation](https://blogs.sans.org/computer-forensics/2010/11/02/digital-forensics-time-stamp-manipulation/).  
  
The post describes how to spot time stamp manipulations when performing a forensic analysis.  
  
The NTFS file system stores the time stamps in two different attributes (**$STANDARD_INFORMATION** and **$FILE_NAME**) and both have the fields Modification, Accessed , Change and Born.  
  
[Dave Hull](https://blogs.sans.org/computer-forensics/author/trustedsignal/) used the **$FILE_NAME** attribute to spot the time stamp manipulations that may be done by tools like  [timestomp](http://www.metasploit.com/research/projects/antiforensics) or [Metasploit](http://www.metasploit.com/).  
  
**$FILE_NAME** is not a standard attribute that can be extracted with all forensics tools, but [Mark McKinnon](http://twitter.com/markmckinnon) has written a tool called mft_parser (not released yet) that can do that.  
  

```
mft_parser_cl <MFT> <db> <bodyfile> <mount_point>
```
> The “db” argument is the name of a sqlite database that the tool creates, “bodyfile” is similar to the bodyfile that [fls](http://www.sleuthkit.org/sleuthkit/man/fls.html) from Brian Carrier’s [The Sleuth Kit](http://www.sleuthkit.org/sleuthkit/) produces, except that it will also include time stamps from NTFS’ $FILE_NAME attribute. The “mount_point” argument is prefixed to the paths in the bodyfile, so if you’re running this tool against a drive image that was drive C, you can provide “C” as an argument.

  
  
Notes:  
* **Bodyfile**: listing of files and directories in a file system, with its time stamps.
