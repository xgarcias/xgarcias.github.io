---
layout: post
title: Building a DNS sinkhole in FreeBSD with Unbound and Dnscrypt
date: '2016-08-25T20:30:00.001+02:00'
author: Xavier Garcia
tags:
- sinkhole
- unbound
- dns
- freebsd
- dnscrypt
modified_time: '2016-08-25T20:42:00.414+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-5873124997748595276
blogger_orig_url: http://www.shellguardians.com/2016/08/building-dns-sinkhole-in-freebsd-with.html
---

There is already lots of literature regarding [DNS sinkholes](https://www.sans.org/reading-room/whitepapers/dns/dns-sinkhole-33523) and it is a [common term](https://en.wikipedia.org/wiki/DNS_sinkhole) in
Information Security. In my case, I wanted to give it a try on FreeBSD 10 but I didn't want to make use of [Bind](https://www.isc.org/) since it was removed from the base distribution in favor of [Unbound](https://www.unbound.net/).

The setup will have the following steps:

-   Create a jail where the service will be configured (not explained
    because there is lots of examples in Internet)
-   Install Unbound
-   Basic Unbound configuration
-   Configure Unbound to block DNS queries
-   Choosing block lists available in Internet
-   Updating the block lists
-   Bonus: use dnscrypt to avoid DNS spoofing
-   Final Unbound configuration file


Configuring our DNS sinkhole
----------------------------


### Installing Unbound

I ran my test in FreeBSD 10.1. Sadly, it ships  Unbound v. 1.4.x, that
is quite old and lacks some nice features. In the end, I had to install
dns/unbound form the ports, that currently installs v.1.5.9.


If you are using a most recent FreeBSD distribution (e.g. FreeBSD 10.3),
you will not need to install the port.


The only difference is that you will need to use **local_unbound_enable="YES"**
in /etc/rc.conf instead of **unbound_enable="YES"** and the configuration file
will be located in **/etc/unbound/unbound.conf** instead of
**/usr/local/etc/unbound/unbound.conf.**


### Basic Unbound configuration

First, we have to download the root-hints, to allow our dns cache to
find the right master DNS servers.

```
# fetch ftp://ftp.internic.net/domain/named.cache -o /usr/local/etc/unbound/root.hints
```

Then, we edit the unbound.conf.
```
server:
        interface: 10.10.10.10

        #who can use our DNS cache
        access-control: 10.10.10.0/24 allow

        logfile: "/usr/local/etc/unbound/logs/unbound.log"
        username: unbound
        directory: /usr/local/etc/unbound
        chroot: /usr/local/etc/unbound
        pidfile: /usr/local/etc/unbound/unbound.pid
        verbosity: 1
        root-hints: /usr/local/etc/unbound/root.hints

#remote-control allows us to use the unbound-control
#utility to manage the service from the command line
remote-control:
        control-enable: yes
        control-interface: /usr/local/etc/unbound/local_unbound.ctl
        control-use-cert: no


```
Please, notice, that all files are located in **/usr/local/etc/unbound/**.
If you are not using the version provided by de ports tree, the base directory will be**/var/unbound/** instead.


The last step is to enable and to start the service

```
# sysrc unbound_enable="YES"

# service unbound start
```

With this setup, we have a basic DNS cache configurated in our network.
Now, you should be able to query the DNS server listening on  10.10.10.10

```
# host www.google.com 10.10.10.10

Using domain server:

Name: 10.10.10.10

Address: 10.10.10.10#53

Aliases: 


www.google.com has address 74.125.68.147

www.google.com has address 74.125.68.105

www.google.com has address 74.125.68.103

www.google.com has address 74.125.68.99

www.google.com has address 74.125.68.104

www.google.com has address 74.125.68.106

www.google.com has IPv6 address 2404:6800:4003:c02::6
```

### Configure Unbound to block DNS queries

The classic trick in DNS sinkholes is to define authoritative zones in
the DNS cache, that will return a defined static IP address
(e.g.127.0.0.2) to identify in the logs (or in network devices) when
somebody is trying to connect to a blocked domain.


In Unbound, it is a bit more difficult because it is only a basic DNS
cache service and lacks some features, but there are some ways around.


**unbound.conf(5)** has the local-zone directive and it is used to
define local DNS zones but we will "abuse it", by dropping all the
queries to these domains. For instance, if we want to drop all the DNS
queries asking for google.com (and subdomains) we need to add the
directive:

```
local-zone: "google.com" inform_deny.
```


This will silently drop the DNS query and it will write an entry in the
log file (**/usr/local/etc/unbound/logs/unbound.log** in our case). The
client will see show the query times out.

```
[1472139065] unbound[28162:0] info: google.com. inform 10.10.10.3@31679 google.com. A IN

[1472139071] unbound[28162:0] info: google.com. inform 10.10.10.3@56551 google.com. A IN
```


To keep a tidy configuration, we will not add this big list of
**local-zone** directives in the main configuration file but we will
include a file thanks to the the **include** directive, that is located
in the **server** section.

```
server:

....
        include: /usr/local/etc/unbound/blackhole.zone
....

```

### Choosing block lists available in Internet

I am using the following URLs that should be considered safe, with
around 23 thousand domains listed.

```
http://mirror1.malwaredomains.com/files/justdomains
https://zeustracker.abuse.ch/blocklist.php?download=domainblocklist
https://ransomwaretracker.abuse.ch/downloads/RW_DOMBL.txt
http://isc.sans.edu/feeds/suspiciousdomains_Low.txt
http://isc.sans.edu/feeds/suspiciousdomains_Medium.txt
http://isc.sans.edu/feeds/suspiciousdomains_High.txt
```


### Updating the block lists

I've written a small shell script that downloads all the lists every
night and reloads the Unbound configuration.


Please, notice that reloading Unbound will also flush the DNS cache. A
good way to do it is:


**Dump the cache**

```
# unbound-control dump_cache > $cache_file
```

Then, download the files with fetch(1) and regenerate
/usr/local/etc/unbound/blackhole.zone


**Reload the configuration**

```
# unbound-control reload
```


**Load the cache dump back in Unbound**

```
# unbound-control load_cache < $cache_file
```


### Bonus: use dnscrypt to avoid DNS spoofing

[Dnscrypt](https://dnscrypt.org/) can be used to avoid some common DNS
attacks by encrypting and signing the DNS queries. All traffic will go
encrypted using the port 443, both TCP and UDP.


Of course, other issues remain, like DNS spoofing at the server end and
the possible logging.


The client is available in the port tree under dns/dnscrypt-proxy and it
is really easy to configure. We only need two parameters: the ip:port
where we want to listen and which server we want to connect to (aka
Resolver)

```
# sysrc  dnscrypt_proxy_enable="YES"

# sysrc dnscrypt_proxy_flags="-a 10.10.10.10:5353"

# sysrc  dnscrypt_proxy_resolver="dnscrypt.eu-nl"

# service dnscrypt_proxy start
```


The final step will be configuring Unbound to forward all the DNS
queries to dnscrypt. This can be done in the **forward-zone** section.

```
forward-zone:

  name: "."

      forward-addr: 10.10.10.10@5353
```


### Final Unbound configuration file

```
server:

        interface: 10.10.10.10

        access-control: 10.10.10.0/24 allow


        logfile: "/usr/local/etc/unbound/logs/unbound.log"


        username: unbound

        directory: /usr/local/etc/unbound

        chroot: /usr/local/etc/unbound

        pidfile: /usr/local/etc/unbound/unbound.pid

        verbosity: 1


        root-hints: /usr/local/etc/unbound/root.hints

        include: /usr/local/etc/unbound/blackhole.zone


remote-control:

       control-enable: yes

       control-interface: /usr/local/etc/unbound/local_unbound.ctl

       control-use-cert: no


forward-zone:

  name: "."

      forward-addr: 10.10.10.10@5353
```
