---
layout: post
title: Starting An Information Security Program
date: '2012-12-17T16:20:00.000+01:00'
author: Xavier Garcia
tags:
- security
- program
modified_time: '2012-12-17T16:20:46.091+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6231739539343461090
blogger_orig_url: http://www.shellguardians.com/2012/12/starting-information-security-program.html
---
Many people have to face the daunting task of starting a security program in their company and in many cases they are not security professionals but rather the guys  doing operations because the small and medium businesses cannot afford a dedicated position. Also, it is probably the case that many of them are sent to a boot camp or training course and then they have to figure out the next steps.

I have to say that I am not a security professional neither, but I have been doing operations for many years and I would like to share my experiences.  Of course you do not have to trust me because I do not have a paper hanging on the wall saying that I am CISSP or something similar. On the other hand, working in the _trenches_ teaches you more than any book or certification.

 The first thing you have to take into account is that buying expensive devices will not make you more secure. They are helpful to mitigate common non-targeted attacks and they will eliminate the standard noise coming from Internet, but a clever attacker will always find ways around. It you want to make an impact, you have to start from the ground up and build a solid foundation. These are my recommendations:

* **Create policies, procedures and standards**. If  all the systems are built in the same way, all the changes are documented and everybody in operations work under the same rules, it will be more difficult to leave  systems running in the network with a configuration that may not be appropriate or with security holes . On the long run, probably they will be an easy target.
* **Use a tool to verify that all the systems comply with the policies**. For example,  all the systems are at the same patch level, they have the same exact configuration, etc,...
* **Log all the configuration changes**. Logging all the changes will allow you to be notified when an unexpected change in the configuration takes place and by whom. On top, it can be automatically reverted.
* **Catalogue your data according its value/confidentiality**. Never store in the same place confidential information and the publicly accessible one. This applies for storage systems and also for servers. i.e. The same servers are hosting the public website, the Intranet and a document management system. Also applies to a storage system that keeps general purpose documents and also confidential information from management, accounting, etc... 
* **Access controls**. Once the data is catalogued and segregated, apply all the needed access controls and network segmentation. Then, keep a log of all the access attempts (successful and failed),  network activity (.i.e. firewall logs and Netflow data from your routers/switches, full packet captures),  application proxies, etc..
* **Get to know what is normal in your environment**. If you know what is normal in your organization,  everything else will be suspicious and you will have all the information to investigate and trace the source.

As you may notice,  applying all these ideas to an organization that has been running for many years without proper security policies is a long journey, but it will be worth the effort.
