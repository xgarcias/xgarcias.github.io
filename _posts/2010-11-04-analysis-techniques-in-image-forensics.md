---
layout: post
title: Analysis techniques in image forensics
date: '2010-11-04T10:13:00.002+01:00'
author: Xavier Garcia
tags:
- forensics
- timeline
modified_time: '2010-11-12T23:24:10.130+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-902642328512304842
blogger_orig_url: http://www.shellguardians.com/2010/11/analysis-techniques-in-image-forensics.html
---
Interesting [article](http://malwaredatabase.net/blog/index.php/2010/10/25/the-botnet-wars-a-qa/) that describes how botnets and the underground market work.  

> In today’s article (which will be a Q&A, a question & answer), I hope to be able to clear up the mystery behind these kits. I have been able to interview experts in the anti-malware world. They will each give their opinion on this particular subject.

Nice [post](http://windowsir.blogspot.com/2010/10/analysis-techniques.html) from the [Windows Incident Response](http://windowsir.blogspot.com/) blog that describes several techniques for analyzing disk images.  
  
[Timeline analysis](http://windowsir.blogspot.com/2010/07/more-timeline-stuff.html)  

> This is a great analysis technique to use due to the fact that when you build a timeline from multiple data sources on and from within a system, you give yourself two things that you don't normally have through more traditional analysis techniques...context, and a greater relative level of confidence in your data.
>
>  As to the overall relative level of confidence in our data, we have to understand that all data sources have a relative level of confidence associated with each of them. For example, from [Chris's post](http://thedigitalstandard.blogspot.com/2010/10/not-so-perfect-keylogger.html), we know that the relative confidence level of the time stamps within the $STANDARD\_INFORMATION attributes within the MFT (and file system) is (or should be) low. That's because these values are fairly easily changed, often through "time stomping", so that the MACB times (particularly the "B" time, or creation date of the file) do not fall within the initial timeframe of the incident. However, the time stamps within the $FILE\_NAME attributes can provide us with a greater level of confidence in the data source (MFT, in this case). By adding other data sources (Event Log, Registry, Prefetch file metadata, etc.), particularly data source whose time stamps are not so easily modified (such as Registry key LastWrite times), we can elevate our relative confidence level in the data.

 Note: [The SANS Computer Forensic](https://blogs.sans.org/computer-forensics) blog [talks](https://blogs.sans.org/computer-forensics/2010/11/02/digital-forensics-time-stamp-manipulation/) about the same subject.  
  
It makes sense because an analyst cannot trust only a single source of information.  We must correlate multiple data sources in order to get the full picture (context) and spot possible manipulations.  
  
  
Timeline Creation  
=================
In systems with many noise does not make sense creating a full timeline because the background noise may cost you more problems than targeting only the areas you are interested in.  

> However, there is a method to my madness, which can be seen in part in Chris's [Sniper Forensics presentation](http://thedigitalstandard.blogspot.com/2010/10/sector-2010-debuting-sf2.html). I tend to take a targeted approach, adding the information that is necessary to complete the picture. For example, when analyzing a system that had been compromised via SQL injection, I included the file system metadata and only the web server logs that contained the SQL injection attack information. There was no need to include user information (Registry, index.dat, etc.); in fact, doing so would have added considerable noise to the timeline, and the extra data would have required significantly more effort to analyze and parse through in order to find what I was looking for.

Feedback loop
=============
Use a knowledge database updated with findings in your previous investigations. Also, sharing information within a team is vital to achieve the goals and be more efficient.  
  
There are also some comments about [RegRipper](http://regripper.net/?page_id=120),  
  

> _RegRipper is a Windows Registry data extraction and correlation tool. RegRipper uses plugins (similar to Nessus) to access specific Registry hive files in order to access and extract specific keys, values, and data, and does so by bypassing the Win32API._

  
This tool can help to automate some analysis in the registry that could indicate compromises, presence of malware, etc.. with the help of the knowledge database.
