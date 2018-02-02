---
layout: post
title: Monitoring Pastebin Leaks
date: '2011-07-01T23:51:00.002+02:00'
author: Xavier Garcia
tags:
- leaks
- pastebin
modified_time: '2012-02-21T10:58:29.326+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6006345376186348510
blogger_orig_url: http://www.shellguardians.com/2011/07/monitoring-pastebin-leaks.html
---
Yesterday I got some time and I wrote a quick script that continuously monitors pastebin.com, looking for interesting keywords.

The script is called [pastebin.py](http://ghosthunter.googlecode.com/svn/trunk/scripts/pastebin/pastebin.py) and accepts a file containing regular expressions, one per line.

It also permits to reload the regular expressions without stopping it by receiving a SIGHUP and to dump to the screen the  pastes we have  already found with SIGUSR1.

This is a sample output:
``` 
./pastebin.py ./file.txt
[!] My PID is: 9475
[!] Loading regular expressions

Dumping stored matches:
[!] Found Match.  http://pastebin.com/raw.php?i=XXXXXXXX :  @aol\.com [33 times] || @yahoo\.com [42 times] || @gmail\.com [729 times] || @hotmail\.com [355 times] || [\w\-][\w\-\.]+@[\w\-][\w\-\.]+[a-zA-Z]{1,4} [5344 times] || @comcast\.net [1 times] || ;
[!] Found Match.  http://pastebin.com/raw.php?i=XXXXXXXX :  @comcast\.net [1 times] || @hotmail\.com [4 times] || @gmail\.com [11 times] || @yahoo\.com [12 times] || [\w\-][\w\-\.]+@[\w\-][\w\-\.]+[a-zA-Z]{1,4} [37 times] || ;
[!] Found Match.  http://pastebin.com/raw.php?i=XXXXXXXX :  [\w\-][\w\-\.]+@[\w\-][\w\-\.]+[a-zA-Z]{1,4} [1 times] || INSERT INTO [1 times] || union.+select.+from [7 times] || ;
[!] Found Match.  http://pastebin.com/raw.php?i=XXXXXXXXX :  @yahoo\.com [2 times] || -- phpMyAdmin SQL Dump [1 times] || @gmail\.com [2 times] || [\w\-][\w\-\.]+@[\w\-][\w\-\.]+[a-zA-Z]{1,4}  [6 times] || INSERT INTO [1 times] || CREATE TABLE [1 times] || ;
[!] Found Match.  http://pastebin.com/raw.php?i=XXXXXXXXX :  -----BEGIN RSA PRIVATE KEY----- [1 times] || ;
End of dump
```

Update: a maintained and improved version of this script can be found in [Monitoring pastebin.com within your SIEM](http://blog.rootshell.be/2012/01/17/monitoring-pastebin-com-within-your-siem/) by [Xavier Mertens](http://twitter.com/#%21/xme). It is written in Perl, but I think you can survive the headache :p

Update: It seems that pastebin.com has changed the HTML layout and the regular expressions in the script need to be changed. Since the script is not maintained, you have to make the changes on your own.
