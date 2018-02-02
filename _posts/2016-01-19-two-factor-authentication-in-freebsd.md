---
layout: post
title: Two-factor authentication in FreeBSD
date: '2016-01-19T15:47:00.002+01:00'
author: Xavier Garcia
tags:
- ssh
- otp
- yubikey
- hotp
- two-factor
- freebsd
modified_time: '2017-12-28T13:48:25.620+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5362809480136693503
blogger_orig_url: http://www.shellguardians.com/2016/01/two-factor-authentication-in-freebsd.html
---
This post discusses the steps needed to configure two-factor authentication in OpenSSH and the particular case of FreeBSD 10.

But, before we go into the details, we have to discuss the different technologies that provide [one-time passwords](https://en.wikipedia.org/wiki/One-time_password).

Hard tokens vs soft tokens
==========================

Two-factor authentication configurations commonly use one thing known (the password) and another owned ( the OTP token). This setup is common in all situations but there are many OTP tokens in the market and the features they provide may vary.

Soft tokens
-----------

They are generally provided as apps in smartphones and [Google Authenticator](https://en.wikipedia.org/wiki/Google_Authenticator) is a well known example.

Hard tokens
-----------

Dedicated devices that calculate the next valid one-time password. RSA tokens and yubikeys are an example in this case.

From a security point of view, hard tokens are preferred because they cannot be easily tempered. On the other side, a smartphone can be compromised and the attacker may be able to access the secret seed that is used to calculate the OTP.

Time-based vs HMAC-based OTP
============================

[OATH](https://openauthentication.org/) is the open standard used to implement one-time passwords and defines two different protocols [Time-based OTP](https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) (TOTP) and [HMAC-based OTP](https://en.wikipedia.org/wiki/HMAC-based_One-time_Password_Algorithm) (HOTP). The main difference is that TOPT uses the current time to calculate the password while HOTP uses the seed plus a table index to point to the last used password.

TOTP is more secure because it only activates a single password every N seconds (30 sec. in case of Google Authenticator) while HOTP must keep  a small number of active passwords that never expire until they are used.

From the security point of view, HOTP will always have a valid password queued that will be valid until it is used. That is a clear drawback compared with TOTP, because the passwords are only valid for a small time window in that case. On top of that, HOTP needs to keep a small window of valid passwords at a given time because the devices will always print the next passwords in the list every time we tell them so, having the risk of going out of sync with the authentication system (e.g. by pressing the button in the token many times without trying to authenticate, we are moving the internal pointer in the device but not the one in the server). 

If we put the pieces together, we will find that an OTP token may support both protocols or only one. The main issue here is that the token needs to run a clock (have a battery) to calculate the time in TOTP. This is easy with the soft tokens (smartphone) but it may not be the case with the hard tokens. In particular, the Yubikeys and derivatives only support HOTP because they are passive devices that are powered by the USB port (they emulate a keyboard).

Implementing HOTP on FreeBSD with a Yubikey
===========================================

Even HOTP is a bit less secure than TOPT I think it is worth the risk compared with using a soft token in my smartphone, because it may be compromised, stolen, etc.. you name it.

#### Install the oath pam module.

```shell
$ pkg install oath-toolkit
```

  

Configure pam
-------------

Add the line below right after pam_unix.so in /etc/pam.d/sshd and comment out all the opie entries.

  
```shell
auth required /usr/local/lib/security/pam_oath.so usersfile=/usr/local/etc/users.oath
```

  

Configure the user accounts
---------------------------

Create the the configuration file /usr/local/etc/users.oath . It will keep the seeds for each user and it is very important to set the permissions to 600 

  
```
HOTP    user1  - 86da9426803815d4499fb6bebfc2d073bd003e7e
```

  

The long hex string is the seed that will be also copied to the OTP token. The value can be calculated with the command below:

  
```shell
$ head -c 1024 /dev/urandom | openssl sha1
```

Update the seed to the Yubikey
-----------------------------

```shell
ykpersonalize -1 -o oath-hotp  -o append-cr -a 86da9426803815d4499fb6bebfc2d073bd003e7e
```

Configure ssh
------------

Add the lines below

```shell
AuthenticationMethods publickey,keyboard-interactive
ChallengeResponseAuthentication yes
PasswordAuthentication no
UsePAM yes
```

  

[AuthenticationMethods](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man5/sshd_config.5?query=sshd_config) tells OpenSSH to force the user to authenticate using the methods listed, one after the other.  In this case, the user needs to use a public ssh key, then the password and finally the OTP. This configuration, actually, produces a three-factor authentication but you can remove publickey if needed.
