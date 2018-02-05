---
layout: post
title: Backing up my Githup repos
date: '2018-02-05T17:45:00.000+01:00'
author: Xavier Garcia
tags:
- twitter
modified_date: '2018-02-05T17:45:00.000+01:00'
---

I am using [runwhen](http://code.dogmap.org/runwhen/) together with  [daemontools](https://cr.yp.to/daemontools.html) to launch and monitor the backup. The run script used by the svc service executes runwhen commands to sleep until the next run (every hour) and then launch the backup script. The service is running in a dedicated [jail](https://www.freebsd.org/doc/handbook/jails.html).



The run script listed below uses some runwhen commands (rw-add,rw-matchand rw-sleep) to wake-up every hour and [setuidgid](https://cr.yp.to/daemontools/setuidgid.html) to run the service with an unprivileged user.

```shell
#!/bin/sh

exec 2>&1

exec setuidgid gitbackup \
rw-add   n d1S             now1s        \
rw-match \$now1s ,M=00     wake         \
rw-sleep \$wake                         \
/home/gitbackup/update.sh
```


The actual backup script that iterates over all the git repos and fetches the changes.
```shell
#!/bin/sh

exec 2>&1

cd /usr/home/gitbackup/backup
echo "===="
date
echo "===="

for repo in `ls -d1 *.git`; do
        cd $repo && /usr/local/bin/git fetch --all
        cd -
done
echo "===="
```

checking the output log
```shell
$ cat /var/service/backups/log/main/current | tai64nlocal
2018-02-05 18:00:00.098641500 ====
2018-02-05 18:00:00.150083500 Mon Feb  5 18:00:00 CET 2018
2018-02-05 18:00:00.180056500 ====
2018-02-05 18:00:00.211689500 Fetching origin
2018-02-05 18:00:01.073738500 From https://github.com/xgarcias/ansible-cmdb-freebsd-template
2018-02-05 18:00:01.073743500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:01.091577500 Fetching origin
2018-02-05 18:00:02.185366500 From https://github.com/xgarcias/ansible-daemontools
2018-02-05 18:00:02.185371500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:02.203049500 Fetching origin
2018-02-05 18:00:04.180310500 From https://github.com/xgarcias/ansible-macbook
2018-02-05 18:00:04.180315500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:04.198104500 Fetching origin
2018-02-05 18:00:06.448429500 From https://github.com/xgarcias/daemontools-dyndns
2018-02-05 18:00:06.448434500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:06.466266500 Fetching origin
2018-02-05 18:00:08.299785500 From https://github.com/xgarcias/daemontools-poudriere
2018-02-05 18:00:08.299790500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:08.321755500 Fetching origin
2018-02-05 18:00:09.749956500 From https://github.com/xgarcias/daemontools-unbound-sinkhole
2018-02-05 18:00:09.749961500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:09.771744500 Fetching origin
2018-02-05 18:00:11.113934500 From https://github.com/xgarcias/elasticsearch-plugin-readonlyrest
2018-02-05 18:00:11.113939500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:11.135774500 Fetching origin
2018-02-05 18:00:12.703191500 From https://github.com/xgarcias/freebsd_local_ports
2018-02-05 18:00:12.703197500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:12.724967500 Fetching origin
2018-02-05 18:00:13.583204500 From https://github.com/xgarcias/xgarcias.github.io
2018-02-05 18:00:13.583209500  * branch            HEAD       -> FETCH_HEAD
2018-02-05 18:00:13.601461500 ====
```

