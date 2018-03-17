---
layout: post
title: Fixing OpenSC after updating to MacOS Sierra
date: '2018-03-17T13:10:00.000+01:00'
author: Xavier Garcia
tags:
- twitter
modified_date: '2018-03-17T13:10:00.000+01:00'
---
Sierra introduced restrictions to the ssh-agent (new version of OpenSSH) by limiting the PKCS#11 libraries that can be loaded to a list of whitelisted directories. As of now, this is public domain because I must be one of the last persons updating from  **El Capitan** to **Sierra**. Yes, I am not an early adopter!

So, until now I had an alias in my .bashrc that was loading my SSH key in the Yubikey to the ssh agent. The alias was just fine but the library is now outside the trusted path, that is "/usr/lib:/usr/local/lib".

```shell
alias load_key="ssh-add -s /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so"
alias unload_key="ssh-add -e /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so"
```

As always, the error message is everything but useful:

```shell
$ ssh-add -s /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so
Enter passphrase for PKCS#11:
Could not add card "/Library/OpenSC/lib/pkcs11/opensc-pkcs11.so": agent refused operation
```

I had to run the ssh-agent in debug mode to understand what was happening (Google is your friend) and the output said: **provider not whitelisted**.

```shell
$ ssh-agent -d -a /tmp/agent.socket
SSH_AUTH_SOCK=/tmp/agent.socket; export SSH_AUTH_SOCK;
echo Agent pid 2918;
debug2: fd 3 setting O_NONBLOCK
debug3: fd 4 is O_NONBLOCK
debug1: type 20
refusing PKCS#11 add of "/Library/OpenSC/lib/opensc-pkcs11.so": provider not whitelisted
debug1: XXX shrink: 3 < 4
```

```shell
$ SSH_AUTH_SOCK="/tmp/agent.socket" ssh-add -s /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so
Enter passphrase for PKCS#11:
Could not add card "/Library/OpenSC/lib/pkcs11/opensc-pkcs11.so": agent refused operation
```

Goggling again, the first hit is the bug report that was opened last year.

[MacOS: cannot use /usr/local/lib/opensc-pkcs11.so (provider not whitelisted)](https://github.com/OpenSC/OpenSC/issues/1008)

At the end, I had to modify my aliases to the library located in the trusted path.

```shell
alias load_key="ssh-add -s /usr/local/lib/opensc-pkcs11.so"
alias unload_key="ssh-add -e /usr/local/lib/opensc-pkcs11.so"
```

The original post where I setup [SSH public key authentication with security tokens](/2016/10/ssh-public-key-authentication-with.html)
