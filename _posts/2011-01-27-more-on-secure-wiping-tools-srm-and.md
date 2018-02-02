---
layout: post
title: 'More on secure wiping tools: SRM and BCWipe'
date: '2011-01-27T13:56:00.000+01:00'
author: Xavier Garcia
tags:
- forensics
- wipe
modified_time: '2011-01-27T13:56:58.544+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5626904378506733140
blogger_orig_url: http://www.shellguardians.com/2011/01/more-on-secure-wiping-tools-srm-and.html
---
This [article](http://computer-forensics.sans.org/blog/2011/01/19/indepth-analysis-srm-bcwipe-unix) from the [SANS Computer Forensics  Blog](http://computer-forensics.sans.org/blog) explains in detail how the secure wiping tools behave from a forensics point of view.

As explained in previous posts, only a tool that can access the raw device can totally wipe any trace of an existing file, because userland tools cannot access the indirect blocs. This trace can help to confirm that a given file was wiped.
