---
layout: post
title: How to Extract Flash Objects from Malicious PDF Files
date: '2011-05-24T10:06:00.000+02:00'
author: Xavier Garcia
tags:
- forensics
- flash
- pdf
- malicious
modified_time: '2011-05-24T10:06:43.681+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4069743481826611011
blogger_orig_url: http://www.shellguardians.com/2011/05/how-to-extract-flash-objects-from.html
---
Nice [post](http://computer-forensics.sans.org/blog/2011/05/04/extract-flash-from-malicious-pdf-files) from the [SANS Computer Forensics Blog](http://computer-forensics.sans.org/blog/) that explains how to extract Flash Objects from malicious PDF  files.

Why using Flash objects on PDF files? The attackers seem to use ActionScript as an alternative to JavaScript to perform the Heap Spray.

This [cheatsheet](http://zeltser.com/reverse-malware/analyzing-malicious-documents.html) is being used in conjunction with  [pdf-parser](http://blog.didierstevens.com/programs/pdf-tools/) or [PDF Stream Dumper](http://blog.zeltser.com/post/3235995383/pdf-stream-dumper-malicious-file-analysis) to extract the objects contained in the PDF.

Once the Flash object has been extracted, [SWFTools](http://www.swftools.org/) is used to dissemble it and proceed with the analysis.

At the end, the author of the post links to [a real life example](http://www.cyberesi.com/2011/04/25/chinas-charm-diplomacy-in-brics-summit-pdf-cve-2011-0611/).
