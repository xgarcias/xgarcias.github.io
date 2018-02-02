---
layout: post
title: DNS Prefetching implications
date: '2011-03-23T10:05:00.000+01:00'
author: Xavier Garcia
tags:
- dns
- high load
- prefetching
modified_time: '2011-03-23T10:05:19.108+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-9218809408550221001
blogger_orig_url: http://www.shellguardians.com/2011/03/dns-prefetching-implications.html
---
[DNS Prefetching](http://www.chromium.org/developers/design-documents/dns-prefetching) can be a nice feature to speed up browsing, but it can cost a big headache and a big bill as well, if you keep a website with many visits.  
  
Via [this post](http://www.pinkbike.com/news/DNS-Prefetching-implications.html) you can learn what happen when your website has many subdomains and these are prefetched for each visit. This is really important if your paying for your DNS services and the number of queries sent matters. Firefox seems to be even worse, because it tries to resolve IPV6 addresses (AAAA query) for each subdomain as well.  
  
It seems that the browsers understand a standard tag that permits to disable the prefetching.  
  
More info on [Controlling DNS Prefetching](https://developer.mozilla.org/en/controlling_dns_prefetching)
