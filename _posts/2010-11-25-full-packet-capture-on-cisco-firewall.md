---
layout: post
title: Full packet capture on Cisco Firewall
date: '2010-11-25T09:31:00.000+01:00'
author: Xavier Garcia
tags: 
modified_time: '2010-11-25T09:31:20.845+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3093850174850465128
blogger_orig_url: http://www.shellguardians.com/2010/11/full-packet-capture-on-cisco-firewall.html
---
Via [opensourceforensics.org](http://www2.opensourceforensics.org/node/123)  
  
Create and fire up the packet capture
=====================================
```
# capture MYCAP interface IFNAME packet-length 1500 buffer SIZE  
```
  

The above command will capture everything; if you want to filter your capture, add an access list, like so:
```
# capture MYCAP interface IFNAME packet-length 1500 access-list 777 buffer SIZE
```

  
Remember to define access-list 777 first. Of course, you can substitute 777 with any other number.

  
Stop the capture
================
```
# no capture MYCAP interface IFNAME
```

  
Retrieve the captured data
==========================
* Point your browser to the firewall SSL URL like so: https://FW-IP-address/capture/MYCAP/pcap  
* Download the pcap file, and open it with wireshark or a similar tool.  
Note: you can also use tftp to get the pcap.

  
Clean-up
========
```
# no capture MYCAP
```
