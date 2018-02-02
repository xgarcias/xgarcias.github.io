---
layout: post
title: Didier Stevens' Malicious PDF Analysis Screencasts
date: '2011-06-22T09:19:00.001+02:00'
author: Xavier Garcia
tags:
- analysis
- pdf
- screencast
modified_time: '2011-06-22T09:25:42.072+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6455415940121521336
blogger_orig_url: http://www.shellguardians.com/2011/06/didier-stevens-malicious-pdf-analysis.html
---
[Didier Stevens](http://blog.didierstevens.com/) has created a web page with all his [screencasts on Malicious PDF analysis](http://blog.didierstevens.com/screencasts-videos/).

The above mentioned [screencasts](http://blog.didierstevens.com/screencasts-videos/) teach the viewer in the use of  his [PDF tools](http://blog.didierstevens.com/programs/pdf-tools/). In a nutshell:

* **pdfid.py** informs about the different kind of objects contained in the PDF document tree: Pages,  Stream,  OpenAction, Javascript. etc.. It permits to quickly flag a suspicious file as malicious, but without looking at its content.
* **pdf-parser.py** can be used to extract the contents of a chosen object. This can be used to inspect objects of interest and  particularly: OpenAction and Javascript objects.
* Its is important to notice that the objects can be compressed and encoded by making use of Filters. This technique can be used to obfuscate the contents of the malicious file and hide them from the view of the antivirus. **pdf-parser.py** permits to revert these filters by using specific flags in the command line.
* Another interesting feature is the **name type normalization**, since the PDF standard permits to encode the characters in the Hex equivalent. This trick would also be useful for antivirus evasion when the engine does not understand the PDF language.

I have also found this [old post](http://blog.didierstevens.com/2008/04/09/quickpost-about-the-physical-and-logical-structure-of-pdf-files/) that Didier wrote in 2008 to explain how a PDF file is structured. If I am not wrong, the example used in the [first exercice](http://www.youtube.com/watch?v=uqsihQ4Xb6E) is a simplified version of the one appearing in the blog post.
