---
layout: post
title: Emulating Zeus DNS Traffic to Test the Defenses
date: '2011-06-14T11:36:00.002+02:00'
author: Xavier Garcia
tags:
- Metasploit
- test defenses
- zeus
modified_time: '2011-06-14T11:38:23.408+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2228161574642823500
blogger_orig_url: http://www.shellguardians.com/2011/06/emulating-zeus-dns-traffic-to-test.html
---
Via [rapid7](http://twitter.com/rapid7) I have found a nice [post](https://community.rapid7.com/blogs/rapid7/2011/06/13/emulating-suspicious-dns-traffic-with-metasploit-framework) that uses [Metasploit](http://www.metasploit.com/) to test how our defenses react when a host is infected with the Zeus trojan.  

In a nutshell,  the author uses the module  **auxiliary/vsploit/dns/dns_beacon**  to resolve a list of DNS  domain names listed in the  [Abuse.ch's Zeus Tracker](https://zeustracker.abuse.ch/). Since these domain names are known to spread malware, our defenses should react and report the incident.

Please, note the difference between resolving the DNS name and connecting to the server to fetch the malware. I might be wrong, but many IDS/IPS systems only flag the connections to the C&C and the dropper, like the [Emerging Threats Signatures](http://www.emergingthreats.net/cgi-bin/cvsweb.cgi/sigs/VIRUS/TROJAN_Zbot).

The IDS/IPS should inspect the DNS traffic in order to flag our tests. The other option is to setup a [DNS Sinkhole](http://isc.sans.org/diary.html?storyid=7930) that redirects these requests, in conjunction with an IDS rule that flags this redirection.
