---
layout: post
title: Linux USB policies
date: '2010-10-07T09:22:00.003+02:00'
author: Xavier Garcia
tags:
- disable usb
- Linux
modified_time: '2010-10-07T10:00:25.663+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4255640160106365858
blogger_orig_url: http://www.shellguardians.com/2010/10/linux-usb-policies.html
---
Many people don't know this, but the Linux kernel allows the administrators to enable/disable the use of USB devices in the system;  per device or with a default policy (that is allow everything by default).  
  

Authorize a device to connect: 
```
$ echo 1 > /sys/bus/usb/devices/DEVICE/authorized
```

Deauthorize a device: 

```
$ echo 0 > /sys/bus/usb/devices/DEVICE/authorized
```

Set new devices connected to hostX to be deauthorized by default (ie:  lock down):

```
$ echo 0 > /sys/bus/usb/devices/usbX/authorized_default
```

Remove the lock down: 
```
$ echo 1 > /sys/bus/usb/devices/usbX/authorized_default  
```
  
  
For more information:  
[http://www.mjmwired.net/kernel/Documentation/usb/authorization.txt](http://www.mjmwired.net/kernel/Documentation/usb/authorization.txt)  
  
  
It is also possible to disable all the storage devices by disabling the kernel module.
  
Just adding the following entry to /etc/rc.local  

```  
rmmod usb_storage
```
