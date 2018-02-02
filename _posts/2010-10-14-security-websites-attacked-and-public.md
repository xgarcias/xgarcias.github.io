---
layout: post
title: Security websites attacked and public disclosure
date: '2010-10-14T11:22:00.004+02:00'
author: Xavier Garcia
tags:
- disclosure
- dos
- spam
- gangs
modified_time: '2010-10-14T18:54:58.953+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4010510056790581169
blogger_orig_url: http://www.shellguardians.com/2010/10/security-websites-attacked-and-public.html
---
Yes, gangs does not like their dirty laundry being made public because they want to keep working anonymously and, of course, they tend to go mad when somebody researches their activities and practices public disclosure.  
  
Past September 23rd, [Brian Krebs](http://krebsonsecurity.com/) published a story called '[I’ll Take Two MasterCards and a Visa, Please](http://krebsonsecurity.com/2010/09/ill-take-2-mastercards-and-a-visa-please/)' that appeared in main stream websites and led to take down the gang's website, that was used as a market place to sell stolen credit cards.  
  
24 hours later, his website suffered a DoS attack with an average of 2.3 Gb and at least one IP address that belongs to Microsoft was involved. As Krebs comments in his article [Pill Gang Used Microsoft’s Network in Attack on KrebsOnSecurity.com](http://krebsonsecurity.com/2010/10/pill-gang-used-microsofts-network-to-attack-krebsonsecurity-com/), turns out that many computers in Microsoft's net-block have been [compromised](http://www.theregister.co.uk/2010/10/12/microsoft_ips_hijacked/) for weeks and used  to route pharmacy spam sites that belong to Russian gangs.  
  
I found particularly funny and ironic this paragraph,  

>  In just one of the many ironies in this story, the compromised server inside of Microsoft appears to have been running Linux, not one of Microsoft’s server technologies. According to Guilmette, all of the hacked servers used by this pill gang are Unix or Linux servers. This mode of operation matches that of “Bulker.biz,” a [rogue pharmacy affiliate program](http://spamtrackers.eu/wiki/index.php/Bulker.biz) known for promoting rogue “Canadian Health&Care Mall” pill sites — as well as a number of other brands — by hijacking poorly-secured Linux and Unix servers.

  
And the answer  from Microsoft,  

> Microsoft became aware of reports on Tuesday, October 12, 2010, of a device on the Microsoft network that was possibly compromised and facilitating spam attacks. Upon hearing these reports, we immediately launched an investigation. **We have completed our investigation and found that two misconfigured network hardware devices in a testing lab were compromised due to human error.** Those devices have been removed and we can confirm that no customer data was compromised and no production systems were affected. We are taking steps to better ensure that testing lab hardware devices that are Internet accessible are configured with proper security controls.
