---
layout: post
title: Use flow data to date and identify an intrussion
date: '2011-01-18T09:36:00.000+01:00'
author: Xavier Garcia
tags:
- flow
- incident response
modified_time: '2011-01-18T09:36:34.446+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4951180336576448757
blogger_orig_url: http://www.shellguardians.com/2011/01/use-flow-data-to-date-and-identify.html
---
One of the key points of  [NSM (Network Security Monitoring)](http://nsmwiki.org/Main_Page) is the use of  flows to track/analyse the network activity in order to response to an incident or perform forensics.  
  
I found the two following posts thanks to [Richard Bejtlich](http://taosecurity.blogspot.com/). They describe how to use the flow data that we can extract from our routers to track and response to an incident.  
  
The [first post](http://blather.michaelwlucas.com/?p=482) explains how to track anomalous activity in our systems thanks to the network activity recorded in the flows. In this case, the attacker planted an IRC backdoor.  
  
The [second post](http://blather.michaelwlucas.com/?p=494) explains how to detect the attack vector by  filtering  the 'known good' traffic.
