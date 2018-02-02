---
layout: post
title: 'When The Comparison Functions Do Not Compare:  The MySQL Fail'
date: '2012-06-11T10:44:00.000+02:00'
author: Xavier Garcia
tags:
- vulnerability
- hash
- memory
- exploit
modified_time: '2012-06-13T09:49:17.095+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6049356316579261575
blogger_orig_url: http://www.shellguardians.com/2012/06/when-compare-functions-do-not-compare.html
---
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">MySQL bypass:<br><br>$ for i in `seq 1 1000`; do mysql -u root --password=bad -h 127.0.0.1 2&gt;/dev/null; done <a href="https://t.co/DiqDFMC1">https://t.co/DiqDFMC1</a><br>/via <a href="https://twitter.com/hdmoore?ref_src=twsrc%5Etfw">@hdmoore</a></p>&mdash; Mikko Hypponen (@mikko) <a href="https://twitter.com/mikko/status/212083731513622529?ref_src=twsrc%5Etfw">June 11, 2012</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


This bug  demonstrates why I hate C so much. It is not enough that you have to be really careful when writing code that you also have to be aware of tricks and optimizations applied by the compilers. I cannot point to details but it is not the first time that something like this happens.

In a nutshell (read this [post](https://community.rapid7.com/community/metasploit/blog/2012/06/11/cve-2012-2122-a-tragically-comedic-security-flaw-in-mysql) from Rapid7) the [memcmp()](http://www.cplusplus.com/reference/clibrary/cstring/memcmp/) function does not behave as expected when gcc uses the SSE optimization. As you may have noticed, I am not an expert in C so do not expect a long and detailed explanation.

The documentation states:

> Compares the first num bytes of the block of memory pointed by ptr1 to the first num bytes pointed by ptr2, returning zero if they all match or a value different from zero representing which is greater if they do not.

There is no warning whatsoever, but it seems that it is not always the case. As H.D. Moore explains  in his post: 

> On some platforms and with certain optimizations enabled, this routine can return values outside of this range, eventually causing the code that compares a hashed password to sometimes return true even when the wrong password is specified. Since the authentication protocol generates a different hash each time this comparison is done, there is a 1 in 256 chance that ANY password would be accepted for authentication.

The exploit? Pretty simple: we try to authenticate in  a for loop until the bug appears.

```shell   
> $ for i in `seq 1 1000\`; do mysql -u root --password=bad -h 127.0.0.1 2>/dev/null; done  
> mysql>
```
  
**Update:** this [post](http://unaaldia.hispasec.com/2012/06/mysql-o-como-es-posible-dar-por-valida.html) from [Hispasec](http://www.hispasec.com/en/) (Spanish) has more information regarding the vulnerability.

It seems the vulnerability would be a truncation from int to char, put together with a compiler optimization.

The function that compares the hash given with the stored in the database can be found in the file  'sql/password.c':

```c
my_bool
check_scramble(const char *scramble_arg, const char *message, const uint8 *hash_stage2)

{
...
return memcmp(hash_stage2, hash_stage2_reassured, SHA1_HASH_SIZE);

}
```

As we can see, [memcmp()](http://www.cplusplus.com/reference/clibrary/cstring/memcmp/) will return an  int, that will be truncated to a char. Therefore, the hash is valid if check_scramble returns the char 0 (non-zero is a wrong hash). As a side note: the type my_bool is defined as char in 'include/my_global.h'.

The patch changes this behaviour to ensure the result. Now, the function check_scramble returns:

```c
return test(memcmp(hash_stage2, hash_stage2_reassured, SHA1_HASH_SIZE));
```

  
being test() a macro defined in include/my_global.h  
  
```c
#define test(a) ((a) ? 1 : 0)
```

This time, we have a boolean operation: return 1 **if the value of 'a' is different to 0** and **return 0 in other case**.
