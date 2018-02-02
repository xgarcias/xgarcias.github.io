---
layout: post
title: Real time Google Hacking
date: '2010-10-11T09:02:00.006+02:00'
author: Xavier Garcia
tags:
- bing
- reader
- google
- hacking
- rss
modified_time: '2010-10-12T08:03:21.290+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5444599336300888362
blogger_orig_url: http://www.shellguardians.com/2010/10/real-time-google-hacking.html
---
Probably everybody knows that Google restricts the searches to prevent people from launching automated searches and finding sensitive data.  The interesting part is that the Google services do not have this restriction, so you could crawl their database to find many dorks. :)  


The guys of  [Pauldotcom](http://pauldotcom.com/2010/10/real-time-google-hacking.html) comment on their blog this behavior. Rob Ragan  and Francis Brown ( the  Bing/Google Hackers  at [Defcon](https://www.defcon.org/html/defcon-18/dc-18-speakers.html#Ragan) ) have  done some  research in search engine hacking  with amazing results. I quote the article,

> They took the entire Google Hacking Database, Foundstone Hacking Database and their new BING Hacking Database and turned them into Google READER RSS feeds. As soon as Google or BING indexes a new site that matches your "intitle:Index Of passwords" criteria Google reader adds it to your RSS feed. (Your Google reader is able to get BING results by leveraging BING's &format=rss parameter) As a result, Google and BING are constantly searching for all the Googledorks in the database and maintaining a realtime database of the results! Then Rob and Francis exported their RSS feeds to OPML format so you can just import them into your own Google reader account.

  
You can find the project website [here](http://www.stachliu.com/index.php/resources/tools/google-hacking-diggity-project/).
