---
layout: post
title: Trying to Tame Selinux
date: '2013-06-19T10:21:00.001+02:00'
author: Xavier Garcia
tags:
- security
- selinux
- easy
modified_time: '2013-06-19T10:23:14.933+02:00'
thumbnail: https://i.ytimg.com/vi/MxjenQ31b70/default.jpg
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7222323361944471413
blogger_orig_url: http://www.shellguardians.com/2013/06/trying-to-tame-selinux.html
---
If you have ever had to fight with Selinux, you know how annoying it can be. In my experience, Selinux is a good layer of security if you have a good knowledge of what your applications can do. A good example would be a DNS or e-mail server, because the code and features they offer barely change.

On the other hand, trying to use Selinux with a complex system like a web application can be a drama unless it is integrated in the development cycle, that will not happen.  These kind of applications change constantly and it requires effort and time to keep the policies updated, without taking into account that the developers will press you because they just want to get things done. As a result, many sysadmins will get pissed off and will opt to simply disable Selinux to have an easy life.

The video below is a presentation that took place in the Red Hat Summit in 2012 and introduces Selinux in REHL 6.

<iframe allowfullscreen="" frameborder="0" height="315" src="http://www.youtube.com/embed/MxjenQ31b70" width="560"></iframe>
