---
layout: post
title: Using static private keys in embedded devices is an epic fail
date: '2011-01-05T14:56:00.002+01:00'
author: Xavier Garcia
tags:
- ssl
- mitm
- embedded
modified_time: '2011-01-05T17:18:42.088+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-55883733007090655
blogger_orig_url: http://www.shellguardians.com/2011/01/using-static-private-keys-in-devices-is.html
---
This  [project](http://code.google.com/p/littleblackbox/) collects private keys extracted from embedded devices and correlate them with the public certificates.  
  
With this information, an attacker can intercept the communications and decrypt the traffic. Furthermore, having the public and private keys,  the attacker can also perform a [MITM](http://en.wikipedia.org/wiki/Man-in-the-middle_attack) attack that cannot be detected by the victim (Not detected by looking at the SSL/SSH layer).  
  

> LittleBlackBox is a collection of thousands of private SSL and SSH keys extracted from various embedded devices. These private keys are stored in a database where they are correlated with their public certificates as well as the hardware/firmware that are known to use those private keys.
> A command line utility is included to aid in the identification of devices or network traffic that use these known private keys. Given a public certificate, the utility will search the database to see if it has a corresponding private key; if so, the private key is displayed and can be used for traffic decryption or MITM attacks. Alternatively, it will also display a table of hardware and firmware that is known to use that private key.
