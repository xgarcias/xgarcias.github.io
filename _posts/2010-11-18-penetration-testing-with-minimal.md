---
layout: post
title: Doing penetration testing with a minimal  footprint
date: '2010-11-18T11:52:00.008+01:00'
author: Xavier Garcia
tags:
- footprint
- hack3rcon
- meterpreter
modified_time: '2010-11-22T15:56:34.872+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3487494261345704013
blogger_orig_url: http://www.shellguardians.com/2010/11/penetration-testing-with-minimal.html
---
This [presentation](http://www.archive.org/download/Hack3rcon2010Videos/Hack3rcon6.mp4) from  [hack3rcon](http://hack3rcon.blogspot.com/) shows how to perform a penetration test that will leave a minimal footprint, thanks to the [Metasploit Meterpreter](http://www.metasploit.com/).  
  
It describes techniques to avoid leaving footprints in:  the Eventlog, the Windows Registry, the Windows Prefetch and  the File System.  
  
Below you can read my notes (almost a copy of the slides)  
  
<iframe frameborder="0" height="281" src="http://player.vimeo.com/video/16204223" width="500"></iframe>  
[Operating in the Shadows Carlos Perez a.k.a Darkoperator](http://vimeo.com/16204223) from [Adrian Crenshaw](http://vimeo.com/user729137) on [Vimeo](http://vimeo.com/).  
  
  
  
Meterpreter
===========
* Runs in memory ( no disk access)  
* Memory scrubbing. Not easy to understand what meterpreter did when analizing a memory image.  
* Windows API access  
* HTTPS, TCP and UDP(DNS)  
* Encrypted traffic (man in the middle, self-generated keys)  
* Can be automated and extended  
  
Why leaving a minimal footprint?
===============================
* Test Incident Response  
* Tests monitoring systems  
* Real world attacks.  
  
Planning
========
* list of targets and goals (business and technical point of views).
    * Interview the client and information gathering
* Enumarate target capabilities
* Physical, SE and network.
* Design an initial plan.
* Modify your plan as you keep advancing.
    * Gather information from the hosts (data and configuration).
    * Modify your plan if something looks out of place.
  
Know your enemy
===============
* First go for the easy targets  
  * They will check the processes running, connections, registry keys, event logs and they may dump the memory  
* Not all companies have an IR team  
* In some companies, the system administrators are also doing security.  
* We can predict what the defenders are going to do  
 
* Their questions:  
    * Process list: Time of creation, Parent PID, owned and command line  
    * Connections: Why is a process like 'notepad' connecting to Internet?  
    * Why is Internet Explorer connecting to a not standard port?  
    * etc.  
* They will create a timeline to investigate the incident.  
  
Event log
=========
* Command and capabilities differ among Windows versions (they also do not record the same data and they use different formats)  
* Event log: binary format  up to windows XP.  XML format to Vista, 7 and 2008  
* The IDs also changed with the new formats  
* We can read from the registry without leaving footprints.  
* We can get the file location, name and configuration out of the registry **HKLM\SYSTEM\CurrentControlSet\Services\**  
* Script 'event_manager' works with the Eventlog from memory: query, clear, etc. It saves the data localy in a csv file.  
* Windows 7 and Windows 2008 can send event logs to other servers by using winrm (ssl and self-generated certificates)  
* A server can collect remote event logs if the Wecsvc service is running  
* Wecsvc can be queried by using wecutil command es  (enum subscriptions)  and gs (enum configurations)  
* Most interesting entries: Scheduled tasks, new/change/remove accounts, stop/start service, logon/logoff, failed logon, add/remove user from a group  
  
Windows Registry
================
* OS settings  
* Group policy settings  
* Application settins  
* Read access is available on most of it  
* With the UAC enabled in Windows 7/2008R2, administrators may not be able to modify registry keys  
* It can be configured to log access to it and the modifications (not set by default and rarely used)  
* ACLs can be placed on registry keys (not set by default and rarely used)  
* Metadata only shows Write an Creation Time, but not Access Time  
* We need special tools to get the Write time: F-Response, EnCase and Open Source (http://www.forensicswiki.org/wiki/Windows_Registry)  
  
Windows Prefetch
================
* Saves a list of the most commonly executed binaries to speed up the booting process. Enabled by default on client operative systems since XP .  
* It shows how many times a file has been executed since it first appeared in the prefetch.  
* %windir%\\prefetch and can only be deleted by the administrator  
* Configuratio saved in the registry  
* Anything we do on the computer will create a file there.  
  
User Assist
===========
* Registry key that saves a counter of the programs executed by Explorer.exe  
* **HCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist**
* Each key name is the name of the executable/shortcut encrypted in ROT-13 (can be easily decrypted)  
* Only the commands executed through the GUI  
  
File System
===========
* 2000,XP and 2003 record the last access time by default  
* Vista, 7 and 2008 do not do that (performance)  
* Cleaning a File MACE will not help since only $STDINFO is modified. The data will remain there.  
* Deleted files and directories can be saved in a Volume Shadow (VSS or snapshots) that is enabled by default  
* Some folders and file types are excluded from the snapshots and this information can be queried.  
  
How To Operate
==============
* Use Meterpreter commands  
* Understand the scripts. Are they uploading/creating files or directories?  
* check if prefetch and Volume Shadows are enabled  
* Do not forget the User Assist key if the GUI is used  
  
Know your Environment
=====================
* check your privileges  
* What is running?  
* What is being logged by EventLog?  
* Is VSS enabled?  
* What tools are they using?  
* Is last Access Time logged?  
  
Clear the Tracks
================
* Sometimes is better to clear the security log even if it is a dead gateway  
* Delete the files and then wipe with  cipher.exe  
* Delete the Volume Shadows after whiping the files  
* Delete prefetch entries in client computers  
  
Execution of Commands
=====================
* Execute from Explorer  
* Use Incognito or Tokens if you are System  
* If you are placing tools, stream them under system executables and execute them from there  
* Use Railgun instead of executables if possible (no write to disk is done because it is injecting DLLs)  
  
Hide your Connections
=====================
* The connections must look 'normal'. Try to behave like a ligitimate user/server would do.  
* Use IPv6 when it is available because people is not looking at it.  
  
Where to Take a Dump
====================
* The files in the temporary folders have weird names.  
* If not able to delete the VSS, check the file extensions and temporary folders.  
* Be carefull what you are writting to disk, because the Antivirus will check the files (vbs,payloads)  
* The duplicate and multi_meter_inject scripts can inject a meterpreter payload onto the memory of a running executable.
