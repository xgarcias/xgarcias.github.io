---
layout: post
title: OpenNTPD, leap seconds and other horror stories
date: '2017-01-03T12:00:00.001+01:00'
author: Xavier Garcia
tags:
- leap
- openntpd
- second
modified_time: '2017-01-03T14:50:23.476+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7433927896636782357
blogger_orig_url: http://www.shellguardians.com/2017/01/openntpd-leap-seconds-and-other-horror.html
---
In case you are not informed, there was a [leap second](https://en.wikipedia.org/wiki/Leap_second) on December 31, 2016. I don't know you, but I've read many horror stories about things going terribly wrong after leap seconds and sysadmins in despair being paged at night. Well, today I am going to share one of those stories with you and I hope it will be terrifying.

Horror story
============

Like diligent sysadmins, we monitor the ntpd services on our servers ([OpenNTPD](http://www.openntpd.org/) in our case) and we will be alerted if a noticeable clock offset happens. Of course, in the event of a leap second,  all the servers should trigger an alert and the corresponding recovery. The leap second was inserted as 23:59:60 on December 31 and the servers slowly **chewed** the difference in around 3 hours.

But... Here comes the horror story. Some of the servers didn't recover at all. The graphs showed that the offset was still around -900 ms ( an extra second was introduced, therefore we were one second behind). At the end we had to restart openntpd as a quick remediation.

Below you can find the status of one of the servers, for reference.

```
$ ntpctl -s all

4/4 peers valid, clock synced, stratum 3
peer
   wt tl st  next  poll          offset       delay      jitter
176.9.31.215 from pool de.pool.ntp.org
    1 10  2 1474s 1502s      -984.909ms     6.266ms     0.175ms
62.116.162.126 from pool de.pool.ntp.org
  *  1 10  2  733s 1640s      -984.824ms     1.105ms     0.126ms
78.46.79.68 from pool de.pool.ntp.org
    1 10  3  888s 1509s      -984.824ms     6.380ms     0.138ms
46.4.54.78 from pool de.pool.ntp.org
    1 10  2 3087s 3098s       105.306ms     6.295ms     0.130ms
```

You may notice that one of the peers has a positive offset and it doesn't make any sense because an extra second was introduced as already explained above. I hope you can smell the stink at this moment because it is quite strong.

Well, digging in the logs I also found the following line:

```
ntpd[1438]: reply from 46.4.54.78: not synced (alarm), next query 3228s
```

Yes,  openntpd was unhappy with that peer and decided to stop the time synchronisation until the issue is solved. **Notice that this is really bad situation because we don't control that peer at all**. The only option is to restart openntpd because we configured a Round Robin DNS record.


I decided to do a bit of research and I went to the openntpd's github repo to read the source code. Particuarly, **src/usr.sbin/ntpd/client.c** . Here,  the NTP packet's status is evaluated against a bit mask to analyse the LI bits (Leap Indicator)

```
(msg.status & LI_ALARM) == LI_ALARM || msg.stratum == 0 || msg.stratum > NTP_MAXSTRATUM)
```

The name LI_ALARM is self explanatory. This bitmask evaluates to true when both bits in the Leap Indicator are set to 1. From the [RFC](https://tools.ietf.org/html/rfc5905):

> LI Leap Indicator (leap): 2-bit integer warning of an impending leap second to be inserted or deleted in the last minute of the current  month with values defined in Figure 9.
> 0     no warning
> 1     last minute of the day has 61 seconds
> 2     last minute of the day has 59 seconds
> 3     unknown (clock unsynchronized)

At this point, I can claim that the peer was totally broken because it ran **for hours** (and it may be still broken at this point) **with the clock unsynchronized** and it hit us in a chain reaction. Well, one may expect a minimum quality but these are the risks that you must accept if you use services ran by others (unless you sign on paper a Service Level Agreement).

To understand how risky it can be, we can look at the page that describes how to [join an ntp pool](http://www.pool.ntp.org/en/join.html). Only an static IP address and a minimum bandwidth is required.  This and a couple of recommendations. Hence, the many hobbyists running their own time servers.

ntp.org is running a monitoring system, that can be queried [online](http://www.pool.ntp.org/scores). The servers with a score lower than 10 will be automatically removed from the pool (mine had -100) and  this is a good measure but good luck if they are already active in your ntpd service. They will cause you trouble until you manually restart the service.



Lessons learned
===============

* Actively monitor the ntp service.
* Monitor the general status: un/synchronized, stratum, num valid peers, etc
* Monitor the offset. I do an average of all peers and then apply abs().
* Plan carefully and search for a reliable ntp source.
* Does your datacenter offer this service? Can you have an SLA?
* Avoid country/region pool at pool.ntp.org because they may be run by hobbyists and will cost you pain, even if ntp.org recommends you do to so. Perhaps running the ntp servers provided by your OS vendor is safer.
* Perhaps buy a [DCF77 receiver](https://en.wikipedia.org/wiki/DCF77) to make your own Stratum 1 server but you may need an external antenna if the datacenter walls are too thick.
