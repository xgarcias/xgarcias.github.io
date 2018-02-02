---
layout: post
title: Bypassing the Corporate Proxy
date: '2013-05-27T14:20:00.000+02:00'
author: Xavier Garcia
tags:
- security
- bypass
- proxy
modified_time: '2013-05-27T14:20:03.783+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4745205887212724096
blogger_orig_url: http://www.shellguardians.com/2013/05/bypassing-corporate-proxy.html
---
This is a [post](http://fmariluis.com.ar/blog/2011/12/27/venciendo-un-proxy-http/) in Spanish that explains how to bypass a corporate web proxy (and its filters) by using standard (not true 100%) Unix tools. In this scenario, the user wants to bypass a proxy (a Windows Proxy) that is using NTLM authentication in order to visit forbidden pages and/or for for privacy reasons.

The following tools are used:
* [cntlm](http://cntlm.sourceforge.net/) is proxy that let our tools go through the proxy by doing the NTLM authentication bits. It will be listening in localhost and behaving like a common HTTP proxy.
* [corkscrew](http://www.agroman.net/corkscrew/) to tunnel SSH traffic over HTTP proxies
* An ssh client to open a Socks proxy in localhost and an ssh server listening on 443.
* A web browser that supports Socks proxies (e.g. Firefox)

The traffic will flow as follows:

Firefox -> ssh client -> corkscrew -> CNTLM -> Corporate Proxy -> SSH server -> Inet.
