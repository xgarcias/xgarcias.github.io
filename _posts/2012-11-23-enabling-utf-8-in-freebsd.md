---
layout: post
title: Enabling UTF-8 in FreeBSD
date: '2012-11-23T14:10:00.000+01:00'
author: Xavier Garcia
tags:
- irssi
- screen
- utf
- freebsd
modified_time: '2012-11-26T17:14:00.008+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1015811725372129037
blogger_orig_url: http://www.shellguardians.com/2012/11/enabling-utf-8-in-freebsd.html
---
Note: this post is just a note to myself so I do not forget how to enable UTF-8 in FreeBSD.

I have not realized until today that FreeBSD does not enable UTF-8 by default, even though it is capable.   I  joined some IRC channels with German speakers some time ago and I always knew there was something wrong in the encoding but I was too lazy to fix it.

Today I had a few minutes to play with the settings in my Screen/Irssi configuration and I could not manage to make it work It is really frustrating... In fact, it was only working when UTF-8 was disabled in Screen, that is a good symptom.

After wondering for a while, a thought it could be the case that the problem comes from the locales, because (in theory) UTF-8 should be enabled everywhere. No!! It was not enabled in my FreeBSD box at home. Searching in Google I found [this post explaining the steps](http://www.b1c1l1.com/blog/2011/05/09/using-utf-8-unicode-on-freebsd/).

The charset has to be enabled during the login process. This means we have to change /etc/login.conf or ~/.login_conf . Since I am only interested in having UTF support in the account running Irssi, I made the change there instead of making a global change.

The config is so easy. Edit  .login_conf in your Home directory.

```:ini
me:\
        :charset=UTF-8:\
        :lang=en_US.UTF-8:\
        :setenv=LC_COLLATE=C:
```

Once this is done, it will only apply to new login sessions, so you have to exit Irssi and also close the Screen session.
