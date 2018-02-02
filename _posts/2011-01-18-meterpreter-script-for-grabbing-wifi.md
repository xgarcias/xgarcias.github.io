---
layout: post
title: Meterpreter script for grabbing Wifi profiles
date: '2011-01-18T09:44:00.000+01:00'
author: Xavier Garcia
tags:
- Metasploit
- wifi
modified_time: '2011-01-18T09:44:35.529+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6843048855416843826
blogger_orig_url: http://www.shellguardians.com/2011/01/meterpreter-script-for-grabbing-wifi.html
---
[Digininja](http://www.digininja.org/) has written a [Metasploit script](http://www.digininja.org/metasploit/getwlanprofiles.php) that grabs all the Wireless profiles from Windows Vista or Windows 7 boxes.  
  
  

> It does this by using the following command to dump all the profiles to the current %TEMP% directory 

```
netsh wlan export profile folder=%TEMP%
```

> Then for each line of the output finding the filename of the profile and downloading it. To tidy up the file is then deleted from the directory.  
> The profiles are stored in the .msf3/logs/scripts/wlan_profiles/ directory.
>
> To re-use the profiles they can be imported into another Windows box by using the following command 

```
netsh wlan add profile filename="the_filename.xml"
```
