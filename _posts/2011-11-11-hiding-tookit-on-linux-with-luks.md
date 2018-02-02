---
layout: post
title: Hiding The Toolkit On Linux With LUKS
date: '2011-11-11T14:16:00.003+01:00'
author: Xavier Garcia
tags:
- pentest
- luks
- incident response
modified_time: '2011-11-14T09:32:39.990+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8987716721292070512
blogger_orig_url: http://www.shellguardians.com/2011/11/hiding-tookit-on-linux-with-luks.html
---
The idea behind this post is making the Incident  Response a little bit more complicated during a pen-test, by hiding our tools in "hidden volumes".

Ideally,  when the hard drive has unpartitioned space, the attacker can create a new partition and encrypt it with [LUKS](http://en.wikipedia.org/wiki/Linux_Unified_Key_Setup) to hide the tools. By doing so, the main file system remains unchanged (no new files are written/modified that can trigger an alert in the HIDS) and it is difficult to spot unless the defenders keep track of the logs that will point to new file systems being mounted.

The procedure would be pretty easy:
* Mount the LUKS volume
* Execute the tool in backround
* Umount the LUKS volume in 'lazy mode'

Reading umount(8) , we can find the flag -l :

> _Lazy unmount. Detach the filesystem from the filesystem  hierarchy now, and cleanup all references to the filesystem as soon as it is not busy anymore.  (Requires kernel 2.4.11 or later.)_

The following script works under the same principle, but it creates a file instead of a partition. In this case, it creates a 300MB file named "volume"  that will contain a ext3 file system encrypted with AES 256.

```shell
#! /bin/sh

function find_device_name {
        losetup -j $1 | awk '{print $1}' | cut -f1 -d ":"
}

function create_raw_vol {
        dd if=/dev/zero of=${1} bs=1M count=$2 &> /dev/null  
}

function create_luks_volfile {
        local raw_vol_dev=""
        raw_vol_dev=`losetup -f`
        create_raw_vol $1 $2
        losetup $raw_vol_dev $1
        echo $3 |cryptsetup  -c aes -s 256 luksFormat `find_device_name $1`  &> /dev/null
        losetup -d `find_device_name $1`
}

function mount_luks_volfile {
        local raw_vol_dev=""
        raw_vol_dev=`losetup -f`
        losetup $raw_vol_dev $1
        echo $3 |  cryptsetup luksOpen `find_device_name $1` $2 &> /dev/null
}

function umount_luks_volfile {
        cryptsetup luksClose ${2} &> /dev/null
        losetup -d `find_device_name $1`
}

vol_name="./volume"
vol_size="300"
mapper_name="hidden_volume"
password="1234"

create_luks_volfile $vol_name $vol_size $password
mount_luks_volfile $vol_name $mapper_name $password
mkfs.ext3 /dev/mapper/${mapper_name}
sleep 5
umount_luks_volfile $vol_name $mapper_name
```
