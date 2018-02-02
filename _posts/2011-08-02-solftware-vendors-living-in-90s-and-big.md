---
layout: post
title: Solftware vendors living in the 90's and the big firewall
date: '2011-08-02T09:44:00.000+02:00'
author: Xavier Garcia
tags:
- vulnerability
- firewall
- rant
- software
modified_time: '2011-08-02T09:44:12.437+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2040537194247605138
blogger_orig_url: http://www.shellguardians.com/2011/08/solftware-vendors-living-in-90s-and-big.html
---
This post is yet another **my software is behind the firewall** rant, you can safely skip it because you wont miss a thing :)

I already twitted about this software vulnerability, but readi ng the vendor response in the [advisory](http://www.zerodayinitiative.com/advisories/ZDI-11-244/) I thought I have to give my two cents.

Basically, their response comes to say that (please note the sarcasm):
_Our software is not meant to be in Internet and it should be safe behind the big firewall of your organization. Therefore, we do not care if we have a **remote buffer overflow that requires no authentication**._

To put it into perspective, the software in question is a licensing server used by many vendors  across the board like: Matlab, Simulink, etc.. and widely deployed in universities and other research institutions, whic h are their main customers.

So, why do I think their response was not appropriated and, perhaps, idiotic?


* One of the main characteristics of their costumers is the openness of their ne tworks, because they have students/researchers that tend to go around and need to use the licensing software from all over the network. What does it mean? **They have no perimeter and the firewall is useless!**

* Since the license server is inside the network and **trusted by the costumer**, chances are that the software is running with privileges in a server that is part of the windows domain. What does it mean? **The vulnerability can be used by an attacker to gain further access to the domain and perhaps gain domain admin. privileges as a side effect.**

* Their answer is so 90's that they let everybody think that they do not care about security and the lack all the skills.

* Since they lack on security skills, perhaps they also lack on secure coding practices and there are more security vulnerabilities hidden in their software.
