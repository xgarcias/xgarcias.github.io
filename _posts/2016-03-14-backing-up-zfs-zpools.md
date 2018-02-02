---
layout: post
title: Backing up ZFS zpools
date: '2016-03-14T12:21:00.004+01:00'
author: Xavier Garcia
tags:
- backup
- zpool
- send
- zfs
- receive
modified_time: '2016-03-14T16:49:09.652+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-842151441505764453
blogger_orig_url: http://www.shellguardians.com/2016/03/backing-up-zfs-zpools.html
---
In this post, I am going to describe the process I followed to configure an offline backup of my home NAS server,  to keep the data in a safe place just in case it breaks. This server is running FreeBSD 10.1 and it has a single zpool.

The procedure is quite simple and consists of three steps.

1. Create another zpool somewhere else where we will synchronise all the data. A USB disk in this example. "raid" is the source zpool and "usbbackups" will be the destination one.
2. Create a recursive snapshot. This will create a snapshot in all the volumes
3. Use zfs send and zfs receive to copy all the data over. In our case, we well execute it periodically via a cron job.

Creating the backup zpool
-------------------------

First, we destroy the partition table and we create a gpt one. da1 is our USB disk

```shell
$ gpart destroy da1
$ gpart create -s gpt da1
```

Then, we create the zfs file system with 4k sectors.

```shell
$ gpart add -a 4k -t freebsd-zfs -l backups da1
```

From now on, we can use our USB disk by pointing to /dev/gpt/backups.

The last step is to create the usbbackups zpool. We use an alternative mount point (/mnt) because after the synchronisation the backed up ZFS volumes may try to use the same mount point the production volumes are using and this may mess up our NAS server.

```shell
$ zpool create -R /mnt  usbbackups  /dev/gpt/backups
```

Creating the snapshots
----------------------

I am using the port sysutils/zfsnap to create daily/hourly snapshots of my ZFS volumes so this part is solved quite easily.

I have setup two cron tasks to create and delete the snapshots respectively. We will do a recursive snapshot off all the volumes at midnight and it will be deleted after 4 weeks.

```shell
10 0 * * *  root    /usr/local/sbin/zfSnap -a 4w -r raid
0  1 * * *  root    /usr/local/sbin/zfSnap -d
```

The snapshots are named using the date plus the expiration time  (used by the script to figure out when the snapshot must be deleted).

As an example:

```
raid@2016-03-14_10.19.42--4w
```

Synchronizing the data to the backup zpool
------------------------------------------

We are going to periodically synchronize all our data, snaphsots included, to our backup zpool. We will take advantage of the existing cron that is creating daily snapshots to use them as the synchronization point. 

First, we have to do the initial synchronization. All data will be copied and it will need quite a bit of time to finish depending on the zpool size, the storage, etc.

We will use the newest snapshot in the system and the destination point is our USB disk. In case the destination system is a network device you can pipe the data to ssh (Internet is full of examples).

```shell
$ zfs send -R raid@2016-03-13_11.05.10--4w | zfs receive -Fdvu usbbackups
```

The newest snapshot can be pulled with the command below. It removes the headers from the zfs command, only displays the snapshot name and finally sorts by snapshot name (the newest will be the first one).

```shell
$ zfs list -H -t snapshot -d 1 -o name -S name raid | egrep "\-\-4w"| head -n 1
```

For the periodic synchronizations  we will do a differential copy. This can be achieved by using two snapshots that exist in the source zpool, the older one also existing in the destination zpool.

I have put together the script below to automate the differential backup once a week, via a cron executions. Notice that the -F flag in the zfs receive will delete all the snapshots in the destination zpool that do not exist in the source one.  You can remove this flag and use other means to clean the old snapshots, if you want to have a different expiration policy in the destination zpool.

```shell
#!/usr/local/bin/bash

# we import/export the destination zpool because we

# have a weak CPU and the USB disk slows the server down.

zpool import -R /mnt usbbackups

LATEST_RAID=`zfs list -t snapshot -H -o name -d1 -S name raid | egrep "\-\-4w" | head -n 1`
LATEST_USB=`zfs list -t snapshot -H -o name -d1 -S name usbbackups| egrep "\-\-4w" | head -n 1`

#a bit of bash fu to replace the  zpool name in the variable.

zfs send -R -i "${LATEST_USB/usbbackups/raid}" $LATEST_RAID | zfs receive -Fdvu usbbackups

# disable the USB zpool

zpool export usbbackups
```

To finish the task, we will run the script every Monday at 4am

```
0  4  *  *  0  root    /root/backup_zfs.sh
```
