---
layout: post
title: DNS block list for malicious web traffic
date: '2011-01-05T12:08:00.000+01:00'
author: Xavier Garcia
tags:
- dnsbl
- web applications
modified_time: '2011-01-05T12:08:40.208+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5732295007510775647
blogger_orig_url: http://www.shellguardians.com/2011/01/dns-block-list-for-malicious-web.html
---
[Mubix from room362](http://www.room362.com/blog/2010/12/23/project-honeypot-http-blocklist-module.html) talks about a new service provided by the [projecthoneypot.org](http://www.projecthoneypot.org/httpbl_api.php).  
  
This new [service](http://www.projecthoneypot.org/httpbl_api.php) offers a [DNS block list](http://en.wikipedia.org/wiki/DNSBL) that identifies search engines, suspicious, harvesters, comment spammers, or a combination thereof.  
> Http:BL is similar, but is designed for web traffic rather than mail traffic. The data provided through the service allows website administrators to choose what traffic is allowed onto their sites. This document describes how to integrate with and take advantage of the http:BL service.

> Developers who build the http:BL service into their software are encouraged to enable users of their software to give back to the Project. Http:BL is only valuable if malicious robots continue to run across the Project's honey pots. As such, developers are encouraged to implement systems which would allow the easy creation of and/or linking to honey pots.
>
> For example, if you are developing a plugin for blogging software, we encourage you to prompt users during creation to provide their a link to a honey pot they have installed or a QuickLink. Your plugin can then drop invisible links to the honey pot throughout the blog site. Again, http:BL's value depends on getting as much data from the honey pot network as possible, and getting that data depends on getting traffic to honey pots. Please keep this in mind as you develop your software.
