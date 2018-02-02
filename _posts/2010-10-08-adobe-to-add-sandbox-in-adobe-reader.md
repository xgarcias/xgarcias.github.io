---
layout: post
title: Adobe to add a sandbox in Adobe Reader
date: '2010-10-08T13:30:00.004+02:00'
author: Xavier Garcia
tags:
- security
- adobe
- sandbox
modified_time: '2010-10-12T08:05:45.656+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7953658033308333157
blogger_orig_url: http://www.shellguardians.com/2010/10/adobe-to-add-sandbox-in-adobe-reader.html
---
[Darknet](http://www.darknet.org.uk/2010/10/adobe-pdf-reader-rewrite-to-include-sandbox-feature/) points out to the sandbox that is being implemented in Adobe Reader and will be available in the next major release.  
  
There is no doubt that this software is the most targeted Windows software nowadays. As [Brian Krebs said](http://krebsonsecurity.com/2010/10/reader-acrobat-patches-plug-23-security-holes/) , the last patch cycle had  23 patches!  
  
Reading the implementation details in [Darknet's post](http://www.darknet.org.uk/2010/10/adobe-pdf-reader-rewrite-to-include-sandbox-feature/):  

> The new Reader design will see core and risky PDF functions such as font rendering, Javascript execution, 3D rendering and image parsing happen within the confines of the application itself, isolating these from the privileges of the operating system.

> This effectively relegates Reader to a new rung of privilege below that if the system user, which stops the application simply accessing key parts of the OS such as the Registry or file system[](http://www.darknet.org.uk/2010/10/adobe-pdf-reader-rewrite-to-include-sandbox-feature/#) as it likes. Instead all such calls will have to go through a trusted broker process if they want to communicate beyond the sandbox.
