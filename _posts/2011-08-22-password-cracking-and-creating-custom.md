---
layout: post
title: Password cracking and creating custom wordlists
date: '2011-08-22T09:49:00.002+02:00'
author: Xavier Garcia
tags:
- cuda
- cracking
- password
- wordlists
modified_time: '2011-08-22T13:02:08.125+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1406687343661160656
blogger_orig_url: http://www.shellguardians.com/2011/08/password-cracking-and-creating-custom.html
---
In this day and age, almost everybody has a good video card that can be used to crack passwords, like Nvidia and the CUDA framework, and it really helps to speed it up.

Yes, I agree that computing power is really helpful, but it cannot beat a good crafted custom wordlist.  Cracking MD5 hashes may be fast, but try doing the same with other hashes :)

My advise is simple. Know your target as good as you can!!  Their culture, their language, their people, what do they do for living, etc... and build a custom dictionary on top of that.

You may also find useful this [old post published by the Pauldotcom crew](http://pauldotcom.com/2008/11/creating-custom-wordlists-for.html).  The idea behind it is using the target's website  for our dictionary since, in theory,  it is a valuable source of  the vocabulary being used inside the company.

I did some tests following the above commented tips and I used [Cryptohaze Multiforcer](http://www.cryptohaze.com/multiforcer.php)  (a CUDA based multihash cracker) to crack the passwords. The results were spectacular and I ended up with a 400MB wordlist (aprox 35M words) and it found many of the passwords  in few minutes :)
