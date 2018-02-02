---
layout: post
title: Analyzing Malicious PDF Files with Peepdf [Spanish]
date: '2011-09-15T12:59:00.000+02:00'
author: Xavier Garcia
tags:
- malware
- pdf
- reverse engineering
modified_time: '2011-09-15T12:59:20.107+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6475637123799441629
blogger_orig_url: http://www.shellguardians.com/2011/09/analyzing-malicious-pdf-files-with.html
---
Via [securitybydefault](http://www.securitybydefault.com/2011/09/analisis-de-un-pdf-malicioso-con-peepdf.html)

[peepdf](http://eternal-todo.com/tools/peepdf-pdf-analysis-tool) is a tool written in Python that analyzes the tree structure in the PDF file. This kind of tool is really helpful to have a first impression and decide whether a PDF file could be malicious or not.

The commented [post](http://www.securitybydefault.com/2011/09/analisis-de-un-pdf-malicioso-con-peepdf.html) uses  [peepdf](http://eternal-todo.com/tools/peepdf-pdf-analysis-tool) to find the objects containing the Javascript code that makes the heap spry and the shellcode.

Once shellcode is extracted, they use a standard debugger to conclude that it downloads  a version of the [Zeus trojan](http://en.wikipedia.org/wiki/Zeus_%28trojan_horse%29)
