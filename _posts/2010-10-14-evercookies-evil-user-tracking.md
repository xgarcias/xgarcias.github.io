---
layout: post
title: 'Evercookies: evil user tracking'
date: '2010-10-14T14:14:00.002+02:00'
author: Xavier Garcia
tags:
- Firefox
- Safari
- evercookies
- chrome
modified_time: '2010-10-15T16:54:49.920+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3352155039728748998
blogger_orig_url: http://www.shellguardians.com/2010/10/evercookies-evil-user-tracking.html
---
Many web browsers permit the users to delete the cookies, and this makes tracking user's behavior  more difficult. But, an evil mind thought that using other storage areas that are not meant for storing cookies could bypass the control mechanisms.  
  
An evercookie is defined as:  

> Evercookie is a javascript API available that produces extremely persistent cookies in a browser. Its goal is to identify a client even after they've removed standard cookies, Flash cookies (Local Shared Objects or LSOs), and others. 

> evercookie accomplishes this by storing the cookie data in several types of storage mechanisms that are available on the local browser. Additionally, if evercookie has found the user has removed any of the types of cookies in question, it recreates them using each mechanism available.

  
  
[Jeremiah Grossman](http://jeremiahgrossman.blogspot.com/) points out in his [article](http://jeremiahgrossman.blogspot.com/2010/10/killing-evercookie-google-chrome-wo.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+JeremiahGrossman+%28Jeremiah+Grossman%29&utm_content=Google+Reader) to an evercookie [demo](http://samy.pl/evercookie/) and to the attempts  made by Dominic White to [defeat](http://singe.za.net/blog/archives/1014-Killing-the-Evercookie.html) this tracking system. Dominic [comments](http://singe.za.net/blog/archives/1014-Killing-the-Evercookie.html) that Firefox should be safe by default (?) but Safari not, and he created shell script that deletes the temporary files.  
  
Apparently,  Jeremiah found a way to remove this cookies in Google Chrome and only using the GUI. It is achieved by disabling the Silverlight and Flash storage settings.
