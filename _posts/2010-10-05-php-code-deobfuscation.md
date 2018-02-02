---
layout: post
title: PHP code deobfuscation
date: '2010-10-05T08:22:00.000+02:00'
author: Xavier Garcia
tags:
- security
- deobjuscation
- php
modified_time: '2010-10-05T08:22:17.787+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8209735224371037465
blogger_orig_url: http://www.shellguardians.com/2010/10/php-code-deobfuscation.html
---
The [zscaler](http://research.zscaler.com/2010/10/php-deobfuscation.html) weblog  describes how to use  Evalhook from Steffan Esser to  deobfuscate PHP code.  
  
They point to the following [article](http://php-security.org/2010/05/13/article-decoding-a-user-space-encoded-php-script/index.html) that explains how the tool works.  
  
From Steffan Esser's article:  

> Whenever encoders like php-crypt have to be analysed the task is usually the same. You take the script, replace all calls to eval() with die() and check what it tries to eval(). When it looks safe you will replace the eval() with the evaluated code and repeat. This is a very stupid and time consuming work, especially when there are multiple wrappers of eval(). Therefore I wrote a short PHP extension called [evalhook](http://php-security.org/downloads/evalhook-0.1.tar.gz) that helps with this task.
