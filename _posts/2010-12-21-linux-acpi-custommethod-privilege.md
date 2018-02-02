---
layout: post
title: Linux ACPI custom_method Privilege Escalation
date: '2010-12-21T11:49:00.008+01:00'
author: Xavier Garcia
tags:
- escalation
- Linux
- acpi
- custom_method
modified_time: '2010-12-21T12:02:23.488+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6960277959353987885
blogger_orig_url: http://www.shellguardians.com/2010/12/linux-acpi-custommethod-privilege.html
---
Past November 13rd  a [fix](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;h=ed3aada1bf34c5a9e98af167f125f8a740fc726a) was commited in the Linux kernel.   For some reason **/sys/kernel/debug/acpi/custom_method** was world writable, allowing any user to inject custom ACPI methods  into the ACPI interpreter tables.  
  
As the [RedHat bug report](https://bugzilla.redhat.com/show_bug.cgi?id=663542) explains, it was introduced in this [commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commitdiff;h=a1a541d86f50a9957beeedb122a035870d602647) (Linux 2.6.33)  


**/drivers/acpi/debug.c**

```c
cm_dentry = debugfs_create_file("custom_method", S_IWUGO,
                acpi_dir, NULL, &cm_fops);
```

**S_IWUGO** is a macro that grants world writable permissions  

**source/include/linux/stat.h**

```c
#define S_IWUGO         (S_IWUSR|S_IWGRP|S_IWOTH)
```
  
The fix changes the permissions to S_IWUSR, that is a macro that grants write access to the owner (root)  
  
An [exploit](http://www.exploit-db.com/exploits/15774/) already exists for this vulnerability.
