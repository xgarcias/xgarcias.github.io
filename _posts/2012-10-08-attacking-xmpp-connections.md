---
layout: post
title: Attacking XMPP connections
date: '2012-10-08T10:18:00.000+02:00'
author: Xavier Garcia
tags:
- mitm
- xmpp
modified_time: '2012-10-08T10:20:03.828+02:00'
thumbnail: https://i.ytimg.com/vi/Fj5kbwqXsqY/default.jpg
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8430027704891701628
blogger_orig_url: http://www.shellguardians.com/2012/10/attacking-xmpp-connections.html
---
[XMPP](http://xmpp.org/about-xmpp/) is a well known protocol used for real-time chat. There are many companies using it, but you already know Facebook and Google because they are the bigger ones.

This protocol has been there for many years, but it seems that just lately (or I was not aware of) some people has started coding tools to perform MITM attacks.

Few weeks ago I came across this nice tool called [XMPPloit](http://www.ldelgado.es/index.php?dir=aplicaciones/xmpploit) that is specially written for Google Talk, even though it is not platform specific.  Its main purpose is to proxy the connection between the user and the legitimate server (once we have already performed the MITM e.g. DNS poisoning)  and force the use of a non-encrypted channel with also the option to force plain-text authentication.

Below you can find a nice demonstration in Youtube:

<iframe allowfullscreen="allowfullscreen" frameborder="0" height="315" src="http://www.youtube.com/embed/Fj5kbwqXsqY" width="420"></iframe>

Last week I also came across a similar tool called [xmppmitm](https://github.com/iamultra/xmppmitm) (via [/r/netsec](http://www.reddit.com/r/netsec) )[](https://github.com/iamultra/xmppmitm), but there is not a lot of information and I have not tested it yet.
