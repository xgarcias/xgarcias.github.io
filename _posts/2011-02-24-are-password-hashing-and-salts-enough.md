---
layout: post
title: Are password hashing and salts enough?
date: '2011-02-24T11:08:00.000+01:00'
author: Xavier Garcia
tags:
- salt
- hash
- brute force
modified_time: '2011-02-24T11:08:09.553+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1591511356527173136
blogger_orig_url: http://www.shellguardians.com/2011/02/are-password-hashing-and-salts-enough.html
---
Nice blog post from [f-secure](http://www.f-secure.com/) that [explains](http://www.f-secure.com/weblog/archives/00002095.html) why using salts to protect our passwords from rainbow tables is not enough.  
  
As a quick resume, the idea behind the blog post is that using salts with hash algorithms like MD5 or SHA* is not enough, because these algorithms are meant for computing speed. Thus, using several GPUs to brute force all the passwords may take only few days.  
  
A possible option to make it more difficult is to use algorithms that are more complex, reducing the number of attempts per second.  
  
The following schemes are recommended:  

* PBKDF2 [http://en.wikipedia.org/wiki/PBKDF2](http://en.wikipedia.org/wiki/PBKDF2). 
* Bcrypt [http://www.openwall.com/crypt/](http://www.openwall.com/crypt/). 
* PBMAC [http://www.rsa.com/rsalabs/node.asp?id=2127](http://www.rsa.com/rsalabs/node.asp?id=2127). 

Furthermore:

> So if you are working with passwords, pick one of the schemes above, determine the number of iterations it takes your server check the password for the desired length of time (10, 200ms, et cetera) and use that. Have a unique salt value and iteration count for each user — anything that forces the attacker to focus on each account separately rather than being able to try against all accounts on each iteration.
