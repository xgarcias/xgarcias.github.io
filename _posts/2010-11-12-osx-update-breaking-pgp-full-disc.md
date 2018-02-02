---
layout: post
title: OSX update breaking PGP full disc encryption
date: '2010-11-12T11:41:00.001+01:00'
author: Xavier Garcia
tags:
- osx
- update
- broken
- pgp
modified_time: '2010-11-12T14:58:06.903+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2193278820504496761
blogger_orig_url: http://www.shellguardians.com/2010/11/osx-update-breaking-pgp-full-disc.html
---
Via [darknet](http://www.darknet.org.uk/2010/11/pgp-users-locked-out-with-latest-os-x-update/) :  
  

> For the past day or so I’ve been seeing endless people tweeting about how the latest Mac OS X update b0rks your Mac if you are using PGP full disc encryption. It’s a pretty nasty bug, but thankfully it can be recovered from fairly easily.  
> If you are just looking for a quick solution, you can:  
> a) Not apply the update ([as recommended by PGP](http://forum.pgp.com/t5/PGP-Announcements/Update-ALERT-PGP-MAC-WDE-Compatibil-ity-Problem-with-MAC-OS-X-10/td-p/40584))  
> b) Decypt your volumes, apply the update, then re-encryp_

  
For the LOL:  
  

> Users of PGP’s Whole Disk Encryption for Macs got a nasty surprise when they upgraded to the latest OS X update once they discovered their systems were no longer able to reboot.  
>   
> It seems that Apple and the Symantec-owned PGP suffered a near-fatal failure to communicate that 10.6.5 ships with a new EFI booter that was incompatible with the encryption software’s boot guard. As a result, the update rendered Macs using WDE as little more than expensive paperweights.  
>   
> “PGP you DO HAVE A FREAKING DEVELOPERS LICENCE FOR APPLE RIGHT???” one outraged user vented here. “YOU CANNOT TEST SYSTEM RELEASES IN ADVANCE???”

A fix was provided yesterday morning by PGP, the details are here:

[Mac PGP WDE customers should not apply the recent Mac OS X 10.6.5 update](https://pgp.custhelp.com/app/answers/detail/a_id/2288)  
  
UPDATE: [H security](http://www.h-online.com/security/news/item/PGP-warns-of-Mac-OS-X-10-6-5-update-1135377.html) also talks about the same problem.
