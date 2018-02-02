---
layout: post
title: Cracking Password-Protected SSH Keys with John the Ripper
date: '2011-06-10T10:48:00.002+02:00'
author: Xavier Garcia
tags:
- ssh
- john
- private keys
modified_time: '2011-07-04T08:25:53.209+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3145362123513695745
blogger_orig_url: http://www.shellguardians.com/2011/06/cracking-password-protected-ssh-keys.html
---
I have just found this [announcement](http://www.openwall.com/lists/john-users/2011/06/09/1) sent by Solar Designer from the [Openwall Project](http://www.openwall.com/).

It seems that they have added support to crack password-prot ected SSH private keys:

> This community-enhanced release integrates preliminary support for several non-hashes, im plemented under Dhiru Kholia's GSoC 2011 project. Specifically, it supports cracking of OpenSSH's passphras e-protected SSH protocol 2 private keys, password-protected PDF files with 40-bit and 128-bit RC4 encr yption, and some password-protected RAR archives.

> Yes, Dhiru's SSH key crac ker includes OpenMP parallelization. There's a limitation, though: this requires OpenSSL 1.0.0 or newer, for thr ead-safety of the interfaces being used. When building or running with older versions of OpenSSL, OpenMP paralle lization in the SSH cracker is automatically disabled. (You can always use MPI instead.)
