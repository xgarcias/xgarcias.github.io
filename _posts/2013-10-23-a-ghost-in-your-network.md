---
layout: post
title: A Ghost In Your Network
date: '2013-10-23T10:57:00.001+02:00'
author: Xavier Garcia
tags:
- pentest
- rogue
- device
modified_time: '2013-10-23T11:17:49.667+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-1120643539910924060
blogger_orig_url: http://www.shellguardians.com/2013/10/a-ghost-in-your-network.html
---
It is common that, in a penetration testing,  the [red team](http://en.wikipedia.org/wiki/Red_team) may also be in charge of assessing the physical security in a company. In such circumstances, many  pentesters try to drop a device on the costumer's network to gain full access.

The effectiveness may be quite high, but it depends on how skilled the defender is. For example, a diligent sysadmin may scan the network every other day, spotting the device soon or later.  What can we do to change this?  How can we hide from the defenders?

It turns out we can use an old trick available in almost all PC devices, that is barely used nowadays and it has been there for ages. All PCs have a [real time clock](http://en.wikipedia.org/wiki/Real-time_clock) that can be programmed to automatically wake-up/boot our computer at a given time in the future.  What if we could drop a device that could sleep for days, waiting for the right moment to wake-up and drop a remote shell? The sysadmins can scan and scan and scan... They will not find it because it only runs for a couple of hours at night!

Imagine the following scenarios:

* A rogue Access Point appearing every night at 10pm from nowhere, that gives direct access to the internal network for 30 min (unless you prevent it from going back to sleep).
* A remote shell to your [Meterpreter](http://en.wikipedia.org/wiki/Metasploit_Project) instance every night to run some scheduled tasks, before disappearing again from the network.
* A rogue device that wakes up to exfiltrate data for a short period of time and then it goes back to sleep for days.

How can we configure our system to behave this way? It turns out its is fairly easy, because we only need to change a  file in our Linux installation. Every time our PC goes to sleep or it shuts down, the system writes the current time into /dev/rtc0 to be sure we are not waking up by mistake. This is a pretty standard behaviour in all Linux distributions. In my case, the tests were done in Ubuntu.

On **/etc/init/hwclock save.conf** , you can find the script that resets the hardware clock. You can see in bold the lines I added to keep the time I had set previously.

```shell
# hwclock-save - save system clock to hardware clock
#
# This task saves the time from the system clock back to the hardware
# clock on shutdown.

description     "save system clock to hardware clock"

start on runlevel [06]

task

script
    . /etc/default/rcS
    [ "$UTC" = "yes" ] && tz="--utc" || tz="--localtime"
    [ "$BADYEAR" = "yes" ] && badyear="--badyear"
    CPITIME=`cat /sys/class/rtc/rtc0/wakealarm`
    exec hwclock --rtc=/dev/rtc0 --systohc $tz --noadjfile $badyear
    echo "$ACPITIME" > /sys/class/rtc/rtc0/wakealarm
end script
```

How can I hook a script to be executed when my device wakes up? To do so, you have to  drop an executable script on /etc/pm/sleep.d/. This script will be executed every time the device wakes up or sleeps and it receives a single parameter to differentiate this circumstance.

```shell
#!/bin/sh

case $1 in
        suspend|suspend_hybrid|hibernate)
                #this code will be executed before we go sleep.
                /usr/local/bin/disable_evil_ap.pl
        ;;
        resume|thaw)
                #this code will be executed when we wake-up.
                /usr/local/bin/enable_evil_ap.pl &

                /usr/local/bin/set_next_wake_up.pl
        ;;
esac

return 0
```

At some point you have to write a **UTC Unix Timestamp**  into **/sys/class/rtc/rtc0/wakealarm**. In the example above we assume it is done by the script **/usr/local/bin/set_next_wake_up.pl.**

At the end, when the task is finished, we have to call the **pm-suspend** command, that will start the suspend to RAM process,. This process will execute again the script above but with **suspend** as the single parameter.
