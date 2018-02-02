---
layout: post
title: 'Auditing logs: tracing e-mail transactions II'
date: '2012-01-04T10:22:00.004+01:00'
author: Xavier Garcia
tags:
- e-mail
- log management
modified_time: '2012-02-22T15:23:26.815+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-2503671544880728346
blogger_orig_url: http://www.shellguardians.com/2012/01/auditing-logs-tracing-e-mail.html
---
In the previous post [Auditing logs: tracing e-mail transactions](http://www.shellguardians.com/2011/12/auditing-logs-tracing-e-mail.html) I talked about a [script](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/search_email_transactions.py) I wrote to make sense of the e-mail logs when doing troubleshooting or just investigating an incident. The downside, of course, is that we have to process all the logs every time the script is ran and this can be time consuming.

To solve this problem I decided to index the 'reduced' data with [elasticsearch](http://www.elasticsearch.org/), that is a search engine based on [lucene](http://lucene.apache.org/java/docs/index.html). As a result, I can make quick searches upon millions of unique e-mail transactions and get a result in a matter of seconds.

Structuring the e-mail transactions
===================================
First of all, I have to clarify that each e-mail transaction is a unique operation in a single e-mail server. Therefore, sending an e-mail may involve several e-mail transactions because it is traversing several e-mail servers throughout our infrastructure. At the end, each of these unique transactions are represented by the following data structure:

* from: A string representing the sender's e-mail address.
* to: Array of recipients. Each element in the array is a dictionary with the following fields:
* recipent: one of the recipient's e-mail address
* relay: the next hop in the delivery chain. It can be a server or local delivery.
* status: A string that informs about the result of the operation.

Since a particular e-mail can be stuck in the queue and re-delivered later, we may see the same recipient appearing several times, but with different status messages: ie. deferred and successfully sent.

* msgid: unique message identifier that represents a particular sent e-mail. Not to confuse with an e-mail transaction that is unique within an e-mail server.
* client: The previous hop in the e-mail chain. 
* date: String representing the time in which the transaction took place.
* host: the server that is executing the e-mail transaction.

Data retention policy
=====================
I have configured the index to automatically drop entries older than 90 days. In my opinion, we do not need to keep this data for a longer period of time, because the troubleshooting tends to involve transactions that took place in the previous days. Of course, In case it is needed, we still keep the raw logs for a longer period and they can be manually parsed or, simply, re-indexed.

Reducing and indexing the raw logs
==================================
The script  [elasticsearch.py](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/elasticsearch/elasticsearch.py) parses the raw logs and indexes them by using the [REST API](http://www.elasticsearch.org/guide/reference/api/).

There is a very dirty hack here, since many syslog servers do not send the year in the log messages. The script assumes we are indexing logs from the current year and makes a dirty trick on January 1st. In case you want to index a log file from the previous year you can use the -y flag to force this case. Yes, it is as dirty as I said :)   Modern syslog servers like rsyslog or syslog-ng can be configured to output the year, but it may not be the case with older installations.

Searching
=========
The script [search.py](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/elasticsearch/search.py) connects to the elasticsearch server and sends the queries.

A query example would be the following one:

```shell
$ ./search.py -f bob@foo.com -d '2011-12-15 00:00:00' -D '2011-12-17 00:00:00' -h smtp -r 10
transaction: pBFERI8l019936
client: bob.desktop [10.10.10.10]
from:   bob@foo.com
msgid:  20111215142718.GD23530@smtp.foo.com
date:   2011-12-15 15:27:19
to:     recipent='alice@bar.com' , relay='smtp.bar.com', status='Sent (Ok: queued as 5298B228B8B)'
host:   smtp

transaction: pBFDdOFC012829
client: bob.desktop [10.10.10.10]
from:   bob@foo.com
msgid:  20111215133924.GC23530@smtp.foo.com
date:   2011-12-15 14:39:25
to:     recipent='alice@bar.com' , relay='smtp.bar.com', status='Sent (Ok: queued as 16F49228B8B)'
host:   smtp
```

The above query searches all the e-mail transactions that match:

* The sender is bob@foo.com
* Between 2011-12-15 00:00:00 and 2011-12-17 00:00:00
* The transactions occur in the server called smtp
* Only output the 10 most recent transactions.


All the scripts can be found [here](http://ghosthunter.googlecode.com/svn/trunk/scripts/log_management/elasticsearch/search.py).
