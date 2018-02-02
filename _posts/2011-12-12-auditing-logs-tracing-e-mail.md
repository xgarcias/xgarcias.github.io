---
layout: post
title: 'Auditing logs: tracing e-mail transactions'
date: '2011-12-12T09:53:00.001+01:00'
author: Xavier Garcia
tags:
- e-mail
- log management
modified_time: '2011-12-20T10:06:15.760+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4804690838334843002
blogger_orig_url: http://www.shellguardians.com/2011/12/auditing-logs-tracing-e-mail.html
---
Every good admin knows that analyzing the log files plays a key role in not only security, but also in the day-to-day IT operations. Who does not read the logs... (sarcasm)?

One of the situations I have to face really often is investigate e-mail problems such: delays, e-mail not arriving, bounces, user account does not exist, etc.. or, simply, whether a user sent an e-mail or not.

If reading the logs created by Postfix or Sendmail is a pain 'per se', trying to understand what happened in a scenario with multiple intermediate servers is a nightmare. Therefore, doing log management is key to succeed (in this particular situation or any other that involves large quantities of data).

There is nothing fancy in my setup. I am just using a centralized syslog server to collect all the raw logs created by the e-mail servers. Then, we can trace the problem from one single place, that is good, but trying to understand what happened is still a pain.  **We still cannot see the forest for the trees.**

I have come up with a Python script ( [search_email_transactions.py](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/search_email_transactions.py) ) that parses Postfix and Sendmail logs. It searches all the e-mail transactions that match the  message id, the sender, the recipient and the date.

The output is self-explanatory:

```shell
$ cat /var/log/all |  ./search_email_transactions.py -l -  -f ^me@foo.com  -i 4EDC80B6.8040107@smtp.foo.com

transaction: E324DA41CA
from:   me@foo.com
msgid:  4EDC80B6.8040107@smtp.foo.com
date:   Dec  5 09:28:42
to:     recipent='you@bar.com' , relay='smtp.bar.com[10.10.10.1]:25', status='sent (250 2.0.0 pB58ShMJ024096 Message accepted for delivery)'
host:   smtp1
```

In this example, it only outputs one unique transaction but in a scenario with multiple servers we should have a listing of all the transactions and all the servers involved, giving us the full picture.

Since it is time and CPU consuming, I am planning to modify this script to treat all the raw logs and dump all this information to a search engine like [elasticsearch](http://www.elasticsearch.org/), making the troubleshooting faster while still having the raw logs in case I need to go deeper.
