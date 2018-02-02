---
layout: post
title: The OpenBSD IPSec stack is possibly backdoored
date: '2010-12-15T08:30:00.002+01:00'
author: Xavier Garcia
tags:
- openbsd
- backdoor
- ipsec
modified_time: '2010-12-15T08:33:54.285+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7597848921907695860
blogger_orig_url: http://www.shellguardians.com/2010/12/openbsd-ipsec-stack-is-possibly.html
---
Yesterday, Theo de Raadt sent an [e-mail](http://marc.info/?l=openbsd-tech&m=129236621626462&w=2) to the openbsd mailing list disclosing the possible existence of a backdoor in the IPsec stack.  
  

> I have received a mail regarding the early development of the OpenBSD IPSEC stack. It is alleged that some ex-developers (and the company they worked for) accepted US government money to put backdoors into our network stack, in particular the IPSEC stack. Around 2000-2001.

> Since we had the first IPSEC stack available for free, large parts of the code are now found in many other projects/products. Over 10 years, the IPSEC code has gone through many changes and fixes, so it is unclear what the true impact of these allegations are.

  
  
The forwarded e-mail is unbelievable...  
  

> Hello Theo,
>
> Long time no talk. If you will recall, a while back I was the CTO at NETSEC and arranged funding and donations for the OpenBSD Crypto Framework. At that same time I also did some consulting for the FBI, for their GSA Technical Support Center, which was a cryptologic reverse engineering project aimed at backdooring and implementing key escrow mechanisms for smart card and other hardware-based computing technologies.  
>   
> My NDA with the FBI has recently expired, and I wanted to make you aware of the fact that the FBI implemented a number of backdoors and side channel key leaking mechanisms into the OCF, for the express purpose of monitoring the site to site VPN encryption system implemented by EOUSA, the parent organization to the FBI. Jason Wright and several other developers were responsible for those backdoors, and you would be well advised to review any and all code commits by Wright as well as the other developers he worked with originating from NETSEC.
>
> This is also probably the reason why you lost your DARPA funding, theymore than likely caught wind of the fact that those backdoors were present and didn't want to create any derivative products based upon the same. 
>
> This is also why several inside FBI folks have been recently advocating the use of OpenBSD for VPN and firewalling implementations in virtualized environments, for example Scott Lowe is a well respected author in virtualization circles who also happens top be on the FBI payroll, and who has also recently published several tutorials for the use of OpenBSD VMs in enterprise VMware vSphere deployments.
>
> Merry Christmas...  
>
> Gregory Perry  
>
> Chief Executive Officer 
>
> GoVirtual Education
