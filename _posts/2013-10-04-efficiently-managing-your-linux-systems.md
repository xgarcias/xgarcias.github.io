---
layout: post
title: Efficiently Managing Your Linux Systems With Spacewalk And Puppet
date: '2013-10-04T14:06:00.000+02:00'
author: Xavier Garcia
tags:
- Linux
- management
- open-source
modified_time: '2013-10-04T14:15:02.967+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7802082153526019191
blogger_orig_url: http://www.shellguardians.com/2013/10/efficiently-managing-your-linux-systems.html
---
Some months ago, I had been given the task to upgrade our home-grown linux management platform. This platform was written around [Kickstart](http://fedoraproject.org/wiki/Anaconda/Kickstart) and worked pretty well for many years but it fell short and now we need something most robust and scalable.

This post describes the tools we have decided to use and why. As always, there isn't a single tool/platform that offers all we needed and we had to combine several of them to achieve the results. The text has been structured based in the needs we had.

Installation of new systems
===========================
Ideally it should be based in [Kickstart](http://fedoraproject.org/wiki/Anaconda/Kickstart) to not rewrite again all the code done in the last years. This shouldn't be a problem because almost all the tools in the market are based in PXE and [Kickstart](http://fedoraproject.org/wiki/Anaconda/Kickstart). To do this, we use the [Cobbler](http://www.cobblerd.org/) tools that come installed with [Spacewalk](http://spacewalk.redhat.com/).

All the inventory, installation, etc.. is done with  [Cobbler](http://www.cobblerd.org/) because it is easy to script and more powerful compared with a simple web GUI.

Patch management and auditing
=============================
[Spacewalk](http://spacewalk.redhat.com/) is probably the 'de facto' tool if you are running RedHat based Linux systems. This tool permits to create groups that is very handy if you want to carry a single action in many systems at one. An example would be, applying a patch in all the integration systems for testing before doing the same in the production systems.

Alternatively, you can use [open-scap](http://www.open-scap.org/page/Main_Page) to verify that all your systems comply with your regulations: mainly patch level and configuration. See also the [OpenSCAP page for RHEL6](https://access.redhat.com/site/documentation/en-US/Red_Hat_Network_Satellite/5.5/html/User_Guide/chap-Red_Hat_Network_Satellite-User_Guide-OpenSCAP.html).

Configuration management
========================
We decided to use [Puppet](http://puppetlabs.com/) instead of [Spacewalk](http://spacewalk.redhat.com/). This is the case because its configuration management tool was too simple and inefficient for our needs. In a nutshell,  you have to push all the configuration files with a web GUI and then add/edit the file permissions (too much manual work), it didn't have template engine, inheritance and other advanced features that are indispensable if you are managing a big data centre.

On the other hand, [Puppet](http://puppetlabs.com/) has a robust template language and inheritance, with many documentation/examples on the web. Many sysadmins are scared when they hear about this tool, because it is known to be complex and difficult to use, but it is quite the opposite unless you are trying to build something extremely big like a SaaS system.

In our setup, we moved all the complexity out off [Kickstart](http://fedoraproject.org/wiki/Anaconda/Kickstart), leaving a 50 lines kickstart file, and we decided to rewrite it with [Puppet](http://puppetlabs.com/) even though it required some extra time to have the new platform ready. In a few weeks of  work, we ported all the code and now we can ensure that all servers in a group are configured  the same way and no unexpected changes are made, changing/updating the configuration of all servers is a matter of a few key strokes and it is really easy to deploy/extend new systems.

Another good point is that [Puppet](http://puppetlabs.com/) is configured with text files and, therefore, it is really easy to use combined with any SCM like Git or Subversion to track back all the changes. In case something goes wrong, it is possible to revert the changes to the previous working version in a matter of seconds and without a big hassle.

Monitoring and alerting
=======================
For monitoring and alerting we decided to keep using our old [Nagios](http://www.nagios.org/) installation, because it has proven to be reliable. [Spacewalk](http://spacewalk.redhat.com/) can do some alerting and monitoring but we didn't trust it for such a critical task.
