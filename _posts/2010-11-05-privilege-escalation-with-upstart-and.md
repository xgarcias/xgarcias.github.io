---
layout: post
title: Privilege escalation with Upstart and the GNU ld dlopen vulnerability
date: '2010-11-05T10:40:00.016+01:00'
author: Xavier Garcia
tags:
- escalation
- ld_audit
- upstart
modified_time: '2010-11-05T12:10:32.616+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7880299785405119055
blogger_orig_url: http://www.shellguardians.com/2010/11/privilege-escalation-with-upstart-and.html
---
As I wrote  in the previous  post [GNUI ld dlopen privilege escalation](http://www.shellguardians.com/2010/10/gnu-ld-dlopen-privilege-escalation.html), we can create world writable files owned by root.  The advisory states that we can create a file to /etc/cron.d/, thus we can gain root privileges by creating an entry that drops a setuid root shell, but it is not the case because Cron checks the permissions and does not allow crontabs with global write permissions (for the group and for others).  
  
Gaining root access is not easy because umask does not allow the execute flag for files. So, we cannot put a file in the PATH that could impersonate a legit binary while it drops a suid shell somewhere in the file system, as a simple example.  
  
There are not many places in a Unix system where we can put a file that is going to be parsed (not executed) by an application that is executed by root and, at the same time, permits to execute arbitrary commands (Cron is not the case as commented above).  
  
An option could be to create the files /etc/profile or /etc/bashrc if they do not exist, because they are going to be sourced by bash when root logs into the server,  but they already exist in many systems and the PoC creates files but does not change permissions.  
  
I have found out that [Upstart](http://en.wikipedia.org/wiki/Upstart), that is being used by many distributions, does not check the permissions when reading the configuration files and it offers directives to execute binaries (like getty, anacron, etc..).  This way,  the attacker can create a configuration file that will instruct Usptart to drop a suid root shell at boot time, thanks to the vulnerability in GNU ld.  
  
  
Privilege escalation
====================

  
The following example only applies for Ubuntu, but it can be modified for other distributions.  
- The upstart configuration files are located in the /etc/init directory and named as XXX.conf  
- The directory is owned by root with 755 permissions  
  
The attacker has to create the file **/etc/init/tty7.conf** by executing the PoC and then write the following content onto it.  

```
start on runlevel[12345]  
exec /bin/bash -c "chown root.root /home/msk/exploit/shell ; chmod u+s /home/msk/exploit/shell"  
```

Where **/home/msk/exploit/shell** is a shellcode that calls **/bin/sh** with **suid(0)/sgid(0)**
  
After rebooting,  /home/msk/exploit/shell will be a binary owned by root and with the setuid permission set
