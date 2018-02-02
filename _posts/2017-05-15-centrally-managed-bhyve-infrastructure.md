---
layout: post
title: Centrally managed Bhyve infrastructure with Ansible, libvirt and pkg-ssh
date: '2017-05-15T17:08:00.001+02:00'
author: Xavier Garcia
tags:
- bhyve
- Ansible
- pkgng
- libvirt
modified_time: '2017-05-16T23:41:15.868+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-600031025551737005
blogger_orig_url: http://www.shellguardians.com/2017/05/centrally-managed-bhyve-infrastructure.html
---
At work we've been using [Bhyve](https://wiki.freebsd.org/bhyve) for a while to run non-critical systems.  It is a really nice and stable hypervisor even though we are using an earlier version available on FreeBSD 10.3. This means we lack Windows and VNC support among other things, but it is not a big deal.

After some iterations in our internal tools, we realised that the installation process was too slow and we always repeated the same steps. Of course,  any good sysadmin will scream "**AUTOMATION!"** and so did we. Therefore, we started looking for different ways to improve our deployments.

We had a look at existing frameworks that manage Bhyve, but none of them had a feature that we find really important: having a centralized repository of VM images. For instance, [SmartOS](https://www.joyent.com/smartos) applies this method successfully by having a backend server that stores a catalog of VMs and Zones, meaning that new instances can be deployed in a minute at most. This is a game changer if you are really busy in your day-to-day operations.

Since we are not great programmers, we decided to leverage the existing tools to achieve the same results. This is, **having a centralised repository of Bhyve images in our data centers.**  The following building blocks are used:


* The ZFS snapshot of an existing VM. This will be our VM template.
* A modified version of [oneoff-pkg-create](https://github.com/danrue/oneoff-pkg-create/) to package the ZFS snapshots.
* [pkg-ssh](https://www.freebsd.org/cgi/man.cgi?query=pkg-ssh&apropos=0&sektion=8&manpath=FreeBSD+10.3-RELEASE+and+Ports&arch=default&format=html)  and [pkg-repo](https://www.freebsd.org/cgi/man.cgi?query=pkg-repo&apropos=0&sektion=8&manpath=FreeBSD+10.3-RELEASE+and+Ports&arch=default&format=html) to host a local FreeBSD repo in a FreeBSD jail.
* [libvirt](http://libvirt.org/drvbhyve.html) to manage our Bhyve VMs.
* The ansible modules [virt](http://docs.ansible.com/ansible/virt_module.html), [virt_net](http://docs.ansible.com/ansible/virt_net_module.html) and [virt_pool](http://docs.ansible.com/ansible/virt_pool_module.html).



Workflow:

* We write a yml dictionary to define the parameters needed to create a new VM:
  * VM template (name of the pkg that will be installed  in /bhyve/images)
  * VM name, cpu, memory, domain template, serial console, etc.
* This dictionary will be kept in the corresponding host_vars definition that configures our Bhyve host server.
* The Ansible playbook:
  * installs the package named after the VM template (ZFS snapshot).e.g. pkg install **FreeBSD-10.3-RELEASE-ZFS-20G-20170515**.
  * uses **cat** and **zfs receive** to load the ZFS snapshot in a new volume.
  * calls the libvirt modules to automatically configure and boot the VM.
* The Sysadmin logs in the new VM and adjusts the hostname and network settings.
* Run a separate Ansible playbook to configure the new VM as usual.

Once automated, the installation process needs 2 minutes at most, compared with the 30 minutes needed to manually install VM plus allowing us to deploy many guests in parallel.

Resources:

* Sample config for FreeBSD [https://people.freebsd.org/~rodrigc/libvirt-bhyve/libvirt-bhyve.html](https://people.freebsd.org/~rodrigc/libvirt-bhyve/libvirt-bhyve.html)
* bhyve driver for libvirt [http://libvirt.org/drvbhyve.html](http://libvirt.org/drvbhyve.html)
* virsh examples [https://wiki.libvirt.org/page/VM_lifecycle#Creating_a_domain](https://wiki.libvirt.org/page/VM_lifecycle#Creating_a_domain)
* migrating VMs w/o shared storage [https://hgj.hu/live-migrating-a-virtual-machine-with-libvirt-without-a-shared-storage/](https://hgj.hu/live-migrating-a-virtual-machine-with-libvirt-without-a-shared-storage/)
* xml reference [http://libvirt.org/formatdomain.html](http://libvirt.org/formatdomain.html)
* Virtual networking [https://wiki.libvirt.org/page/VirtualNetworking](https://wiki.libvirt.org/page/VirtualNetworking)
