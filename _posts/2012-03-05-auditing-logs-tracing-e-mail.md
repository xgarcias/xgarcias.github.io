---
layout: post
title: 'Auditing logs: tracing e-mail transactions III'
date: '2012-03-05T20:14:00.005+01:00'
author: Xavier Garcia
tags:
- e-mail
- log management
modified_time: '2012-03-06T09:25:10.036+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2016373518392458684
blogger_orig_url: http://www.shellguardians.com/2012/03/auditing-logs-tracing-e-mail.html
---
Previous posts:

* [Auditing logs: tracing e-mail transactions I](http://www.shellguardians.com/2011/12/auditing-logs-tracing-e-mail.html).
* [Auditing logs: tracing e-mail transactions II](http://www.shellguardians.com/2012/01/auditing-logs-tracing-e-mail.html).

In the two previous posts I described how I made sense of my e-mail logs, [by parsing and storing them](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/elasticsearch/) in a search engine called [elasticsearch](http://www.elasticsearch.org/). This transformation helped me to quickly trace problems in a distributed environment with many servers. Of course, the alternative was  to manually grep the logfiles, which is a waste of time. In this closing post, I would like to present the last tweak I have made in the script and the conclusions after some months of tests.

The previous version was reading all the logs from a file (ie, the syslog file) to store the transactions in the elasticsearch index.  It is handy if we have to start indexing from scratch, but it is quite inefficient if we need to keep the index up-to-date because, when executing the script with Cron, we keep reading/storing the same transactions again and again.

At the same time I was writing this script, I started using [graylog2](http://graylog2.org/) to keep a short term cache of my logs in order to speed up searches and also to use their nifty GUI as well:)  As a side effect, they were using [elasticsearch](http://www.elasticsearch.org/), which helped me to continue using my scripts, which is nice.  As you may already notice, this offers new possibilities, like querying the graylog2 index with the [REST API](http://www.elasticsearch.org/guide/reference/api/), that permits to search by keywords and time frames.

As a result, I updated the [script](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/elasticsearch/elasticsearch.py) to query the [graylog2](http://graylog2.org/) index and extract all the postfix/sendmail logs given a time frame (60 minutes by default). This change helps a lot to reduce the load when it is executed by Cron and, at the same time, it permits to call it in smaller periods of time (ie, every 15 minutes).

Conclusions
===========
By using available tools, we can greatly improve our capacity to resolve incidents, while, at the same time, doing it on a budget. The alternative would be spending hours grepping log files and trying to understand what happened, which is not an easy task.

This post is just using e-mail logs as an example, but this can also be applied to other raw data.  One possible option would be parsing the logs of the firewalls, netflow, IDS, HIDS,etc. running in our infrastructure and storing them in a structured way, so we can do searches to investigate an ongoing incident. Buy doing so, it would help us to correlate the alerts and to find until which extent and attacker has penetrated in our network.

This concept is similar to the way [Sguil](http://sguil.sourceforge.net/) handles incidents happening in our network.  I like the idea of being able to jump between IDS alerts, netflow and Pcap files so easily, because it gives lots of visibility to the analyst and helps to make an informed decision.

Before I finish, I would like to talk a bit about the drawbacks.  Parsing the data and doing some automation is really useful and it greatly helps to solve incidents faster (it is really difficult to find somebody that disagrees), but the picture you have of what is happening is as good as your regular expressions. Yes, the more complex the data is, the more pain you will suffer and you may miss some parts of the picture.  You have to be aware and you may find yourself checking the logs from time to time :)
