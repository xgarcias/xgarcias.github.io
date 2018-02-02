---
layout: post
title: Why I do not trust the cloud
date: '2011-05-05T11:28:00.000+02:00'
author: Xavier Garcia
tags:
- stupidity
- fail
- amazon
- cloud
modified_time: '2011-05-05T11:28:18.561+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8789734455594400501
blogger_orig_url: http://www.shellguardians.com/2011/05/why-i-do-not-trust-cloud.html
---
This [post](https://forums.aws.amazon.com/thread.jspa?threadID=65649&tstart=0) in the [Amazon forums](https://forums.aws.amazon.com/) is so impressive in many senses. It comes to explain how cloud computing and a bad engineer can put  human lives and the business into risk.  
  
Somebody was clever enough to put a critical service like a **cardiac patients monitoring system** on the cloud, without any kind of backup. Yes, it sounds so bad for many reasons...  
  
It turns out that Amazon EC2 went down for some days and the company had all the critical services installed there, without any kind of backup system in another datacenter or whatsoever.  I understand they decided to go **to the cloud** because it was way cheaper compared with maintaining their own infrastructure, but without playing attention to the possible problems, requirements and regulations they have to comply with.  
  
This is a good example to present to the decision makers when they discuss about moving parts of the infrastructure to cloud services or setting up its own infrastructure. It may be good for the business in a short term, but be prepared for the problems.
