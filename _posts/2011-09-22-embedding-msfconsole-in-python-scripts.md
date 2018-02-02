---
layout: post
title: Embedding Msfconsole in Python scripts through the XMLRPC interface
date: '2011-09-22T20:04:00.000+02:00'
author: Xavier Garcia
tags:
- Metasploit
- Python
- xmlrpc
modified_time: '2011-09-22T20:04:20.717+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7167277497760302137
blogger_orig_url: http://www.shellguardians.com/2011/09/embedding-msfconsole-in-python-scripts.html
---
During the last days I have been playing with the Metasploit's XMLRPC interface and I have had lots of fun! :)  
  
I have created a set of Python classes that permit to interact with Metasploit in different ways, hiding the complexity of the the XMLRPC calls.  
  
  
MsfBatch
========
This class permits to launch non-interactive jobs in Metasploit, which will be ran in backgroud.  
  
  
MsfConsole
==========
This class permits to embed a full Metasploit console in your Python script. It also offers a bit of automation, because it permits to launch some tasks in background or foreground before we start interacting the console.  
  
  
  
  
Examples
========
The following code launches an auxiliary module to find which SSH version is running a particular server. This script launches the task and then starts interacting with the created console  

```python
#! /usr/bin/env python  
  
import signal  
from pymsf import pymsf  
import os  
import sys  
  
  
def signal_controlc(signal,frame):  
	myconsole.destroy()  
  
  
myconsole = pymsf.MsfConsole()  
myconsole.login("msf","123456")  
myconsole.create_console()  
  
  
opts = {  
"RHOSTS": sys.argv[1],  
}  
print "launching"  
signal.signal(signal.SIGINT, signal_controlc)  
myconsole.aux("auxiliary/scanner/ssh/ssh_version",opts,True)  
myconsole.interact()  
myconsole.destroy()  
```

 
Output  
```
# ./version.py 127.0.0.1  
launching  
  
                |                    |      _) |  
 __ \`__ \   _ \ __|  _\` |  __| __ \  |  _ \  | __|  
 |   |   |  __/ |   (   |\\__ \ |   | | (   | | |  
_|  _|  _|\\___|\\__|\\__,_|____/ .__/ _|\\___/ _|\\__|  
                              _|  
  
  
       =[ metasploit v3.7.2-release [core:3.7 api:1.0]  
+ -- --=[ 699 exploits - 361 auxiliary - 54 post  
+ -- --=[ 224 payloads - 27 encoders - 8 nops  
       =[ svn r12982 updated 94 days ago (2011.06.20)  
  
Warning: This copy of the Metasploit Framework was last updated 94 days ago.  
         We recommend that you update the framework at least every other day.  
         For information on updating your copy of Metasploit, please see:  
             http://www.metasploit.com/redmine/projects/framework/wiki/Updating  
  
RHOSTS => 127.0.0.1  
[*] 127.0.0.1:22, SSH server version: SSH-2.0-OpenSSH_5.4p1 FreeBSD-20100308  
[*] Scanned 1 of 1 hosts (100% complete)  
[*] Auxiliary module execution completed  
  
msf auxiliary(ssh_version) >  
``` 
  
  
The following code launches batch jobs in our running Metasploit console, trying to login to a SSH server. The script keeps waiting until the job has finished and then lists the existing sessions in case we have created a new one.  

```python 
#! /usr/bin/env python  
  
from pymsf import pymsf  
import os  
import sys  
from time import sleep  
  
  
batch = pymsf.MsfBatch()  
batch.login("msf","123456")  
  
opts = {  
"RHOSTS": sys.argv[1],  
"RPORT": "22",  
"USERNAME": 'root',  
"PASSWORD": sys.argv[2],  
"THREADS": "8",  
"USER_AS_PASS": 'false',  
"BLANK_PASSWORDS": "false"  
}  
  
batch.aux("scanner/ssh/ssh_login",opts)  
before=batch.numSessions()  
batch.waitJobsFinished()  
if before < batch.numSessions():  
	print "New session created. Listing opened sessions"  
	batch.listSessions()  
  
print "Finish"  
```
  
Output  
```
./login.py 127.0.0.1 toor  
New session created. Listing opened sessions  
auxiliary/scanner/ssh/ssh_login  :: 127.0.0.1  
Finish
```
  
The code can be found [here](http://ghosthunter.googlecode.com/svn/trunk/metasploit/pymsf/)
