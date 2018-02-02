---
layout: post
title: Snort  coverage for the Exim  remote root vulnerability
date: '2010-12-14T16:47:00.000+01:00'
author: Xavier Garcia
tags:
- vulnerability
- snort
- exim
modified_time: '2010-12-14T16:47:01.246+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3907780838209330453
blogger_orig_url: http://www.shellguardians.com/2010/12/snort-coverage-for-exim-remote-root.html
---
The [Sourcefire VRT](http://vrt-sourcefire.blogspot.com/) has published a [blog post](http://vrt-sourcefire.blogspot.com/2010/12/exim-remote-root.html) that describes how Snort detects the Exim root vulnerability.  

> Based on what hit the Exim-dev mailing list, we felt confident that the SMTP preprocessor would catch the vulnerability; after testing with the [proof-of-concept](http://seclists.org/fulldisclosure/2010/Dec/221) sent to the Full-Disclosure mailing list on Saturday, we've confirmed that SID 124:2:1 does the job nicely

> No configuration is necessary; the default settings for the SMTP preprocessor will work here. For anyone who may have tweaked their config, ensure that the meax_header_line_len is set to 2000 bytes or less (a reasonable value for all but the most unique of environments; the default value is 1000 bytes).
