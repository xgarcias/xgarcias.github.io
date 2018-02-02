---
layout: post
title: Why is Metasploit flagged by the AVs?
date: '2011-05-05T13:44:00.001+02:00'
author: Xavier Garcia
tags:
- Metasploit
- antivirus
- detection
modified_time: '2011-05-05T13:50:19.964+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4080047661211811077
blogger_orig_url: http://www.shellguardians.com/2011/05/why-is-metasploit-flagged-by-avs.html
---
Nice [article](http://www.scriptjunkie.us/2011/04/why-encoding-does-not-matter-and-how-metasploit-generates-exes/) from [Scriptjunkie](http://www.scriptjunkie.us/) that explains why the Metasploit binaries are being flagged by the AVs.  
  
As I understand,  a Metasploit binary is an executable that creates a RWX memory area, loads the encoded shellcode onto it and then it transfers the execution. Therefore, the AVs are not analyzing the encoded shellcode for the detection, but the executable being used to load the shellcode.  
  
A possible solution would be patching another binary of your choosing, but the AVs may flag it as well because it is creating a RWX memory area and then pointing the IP there, which is really suspicious.
