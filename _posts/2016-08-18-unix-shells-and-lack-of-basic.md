---
layout: post
title: Unix shells and the lack of basic understanding
date: '2016-08-18T16:06:00.001+02:00'
author: Xavier Garcia
tags:
- ifconfig
- exploit
- unix
modified_time: '2016-08-18T16:52:53.458+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1007005660688831917
blogger_orig_url: http://www.shellguardians.com/2016/08/unix-shells-and-lack-of-basic.html
---
It is not news if I say that some major firewall vendors have been owned for years and the exploits have been leaked to the Internet this week. Just search for "Equation Group" and you will be amused.

What pisses me off is one particular privilege escalation for Fortinet Watchguard, that seems to be like wizardry for many people. I have even read comments in my Twitter timeline that made no sense at all and were so wrong that I wanted to rip my eyes.

The vulnerability seems to be located in the restricted CLI, if I am not mistaken, because it doesn't validate the user input when ifconfig is executed.

```shell
$ ifconfig "$(bash -c 'touch /tmp/test; echo -n eth0')"
```

Here comes the thing: many people are claiming that ifconfig is broken because it is executing bash commands. I have even read comments saying that echo is also broken.
**All these people should quit their jobs and go back to the university to learn how a Unix shell works**.

It is a very basic concept. Any thing under double-quotes is interpreted by the shell before the command  (ifconfig in our example) is executed.  Read the [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html#Double-Quotes) for more information.

My guess, because I don't have the source code, is that the CLI was executing the full command via the system() function or similar, without validating the user input. In practice, system() will invoke sh(1) that then will interpret the code enclosed in double-quotes.

* ifconfig "$(bash -c 'touch /tmp/test; echo -n eth0')"
  * system()
    * sh
      * bash
        * touch /tmp/test
        * echo -n eth0

**TL;DR we have seen the same mistake happen again and again since the 90's, when the script kiddies were abusing badly written CGI scripts. Some people will never learn.**

Edit: I originally claimed that the privilege escalation exploit is for Fortinet but it actually targets Watchguards firewalls. See [here](https://www.secplicity.org/2016/08/16/nsa-equation-group-exploit-leak-mean/).
