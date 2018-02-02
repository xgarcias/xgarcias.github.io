---
layout: post
title: bad password implementations and brute-force attacks
date: '2011-03-17T13:53:00.003+01:00'
author: Xavier Garcia
tags:
- brute-force
- password
- seed
modified_time: '2011-03-17T15:52:27.026+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-155364695224057474
blogger_orig_url: http://www.shellguardians.com/2011/03/bad-password-implementations-and-brute.html
---
These serie of posts [ [1](http://www.skullsecurity.org/blog/2011/hacking-crappy-password-resets-part-1) , [2](http://www.skullsecurity.org/blog/2011/hacking-crappy-password-resets-part-2) ]  from [SkullSecurity](http://www.skullsecurity.org/blog/) is really enlightening.  
  
I understand that the main error here is using a **_small_** seed.  I am not an expert , but I understand that the number of possible passwords (the universe) directly depends on the used seed. Therefore, if we use 1,000,000 as a seed, we will have only have one million passwords, that can be easily pre-calculated (a pair of password, md5-hash) and used in an offline attack with John the Ripper.  
  
  
The attack in the second post is fairly similar, but it ends up with a really small universe of only 15,993 possible passwords, due a really bad implementation, that even permits an easy and successful online attack.  
  
The attack consists of grabbing  the HTML output corresponding of a failed login and then comparing the HTML output of each brute force attempt against it. It the md5sum does not match, the password is valid.
