---
layout: post
title: DLP is the next Silver Bullet
date: '2011-03-09T13:18:00.000+01:00'
author: Xavier Garcia
tags:
- dlp
- silver bullet
modified_time: '2011-03-09T13:18:07.894+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3243789776350890457
blogger_orig_url: http://www.shellguardians.com/2011/03/dlp-is-next-silver-bullet.html
---
I think I really do not need to explain what [DLP](http://en.wikipedia.org/wiki/Data_loss_prevention_software) is, unless you have been disconnected for many years.  

I was astonished when I first read this [post](http://isc.sans.edu/diary.html?storyid=10147&rss) from [the Internet Storm Center](http://isc.sans.edu/). The post describes a setup of Snort running in  a bridge and inspecting the traffic between the Corporate Network and the border router (fair enough).  


Then, the following rule is used as an example to catch a possible data ex-filtration.  

```
alert ip 192.168.1.0/24 any -> any any (msg:”Data Loss from inside the network”; content:"Company X - Confidential"; rev:1)
```

I am not an expert in security and you do not have to trust my words, but I think that deploying a device in front of the border router and with this kind of signatures, is only going to catch the more _Naive_ users.  

A skilled attacker will encode/encrypt/partition the data and will **act** like a normal user in order to bypass this kind of rules. Therefore,  we are just having a false sense of security.  

I think, the only way to detect a skilled attacker is by knowing your network and applying the ideas explained in  this book  from [Richard Bejtlich](http://taosecurity.blogspot.com/): [Extrusion Detection: Security Monitoring for Internal Intrusions](http://www.amazon.com/gp/product/0321349962/)
