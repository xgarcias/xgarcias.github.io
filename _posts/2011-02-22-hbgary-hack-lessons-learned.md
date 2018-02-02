---
layout: post
title: 'HBGary hack: lessons learned'
date: '2011-02-22T10:12:00.000+01:00'
author: Xavier Garcia
tags:
- hbgary
- lessons learned
modified_time: '2011-02-22T10:12:44.101+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4101182933821376850
blogger_orig_url: http://www.shellguardians.com/2011/02/hbgary-hack-lessons-learned.html
---
Nice post from the [Internet Storm Center](http://isc.sans.edu/) that [analyzes](http://isc.sans.edu/diary.html?storyid=10438&rss) the  **HBGary Federal hack** and highlights the mistakes.
  
I quote,  
  
  

> A lot of things that we already preach (or should be preaching):
> 
> * Do not use same passwords for multiple applications/sites. A lot of free, good utilities, such as Password Safe exist that will allow you to automatically generate strong passwords and store them in an encrypted key chain.
> 
> * No matter if your company is big or small, you should have change management processes that require all changes to be approved by appropriate personnel. While a CEO can request your administrator to open a port on the firewall, really the security person in charge should approve that. If you don’t have multiple roles for this then make sure that appropriate authentication is in place – i.e. verifying such critical requests through other channels.
> 
> * You should regularly test your web applications – not only external, but also internal. While this does not guarantee that you will identify and eliminate all security vulnerabilities, it will certainly raise the overall security.
> 
> * Encrypt your backups and think twice if you need all those e-mails at one place. Gmail is certainly attractive for storing years of e-mails and searching through them quickly, but imagine what would happen if someone gets access to all your e-mail.
> 
> * When we’re at encryption – encrypt sensitive e-mails too. While it is a nuisance, it can save the day and PGP is not that hard to use. There are downsides, of course, so you should balance between usability and security.
> 
> * If you are a web application developer, and have a need to store (hashed) user passwords remember that algorithms such as MD5 were built for speed! By using today’s GPUs, it is possible to crack hundreds of millions of MD5 passwords per second. Besides this, remember to salt the passwords to make rainbow tables useless (otherwise it’s usually a matter of seconds).
> 
> * Finally, when talking about storing hashed passwords, try to use multiple algorithms to store passwords – something like sha1(sha1(sha1(password))) will still be unnoticeable for your application’s users and at the same time you not only made rainbow tables useless but increased time need for cracking as well (and the attacker will have to make a custom cracking module for his program).
