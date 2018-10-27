---
layout: post
title: Infrastructure monitoring and the journey to the cloud
date: '2018-10-27T10:00:00.000+02:00'
author: Xavier Garcia
tags:
- AWS
- migration
modified_date: '2018-10-27T10:00:00.000+02:00'
excerpt_separator: "<!--more-->"
---
At work we are in the process of moving from a datacenter centric infrastructure to AWS. This is a great journey with many interesting challenges and today we will discuss one of them, **the monitoring of our infrastructure**.

<!--more-->

Taking into account we are quite busy, dedicating resources and money to prototype and later migrate to a new monitoring platform is not high priority unless we detect important gaps. **"If it works, don't touch it", they said.**

Well, at the moment we have a quite stable monitoring stack that meets our requirements but it's obvious that it doesn't adapt well to the cloud, that is very dynamic by nature, because the current monitoring stack relies on manual changes in configuration files and commits to the software repo.

Current setup
=============

We are using Munin for graphing, that also forwards the alerts to our Icinga satellites, that are running in different locations. The setup is great right now, but we have identified the following gaps:

* Very static configuration. We still could use the AWS SDK to rebuild the configuration file automatically, but that could potentially cause other issues, because Munin is quite sensitive when it comes to syntax errors.
* Munin doesn't scale because it's written in Perl. The fact that it needs to run every 5 minutes is a good indicator.
* It also relies in lots of dependencies and scripts in the client. For instance, it cannot be used to monitor Docker containers or cloud managed services, like RDS.
* Having a graph resolution of 5 minutes is not a big drama but it's not usable if we want to do application instrumentation.

Searching for the right solution
================================

Going full managed
------------------

A simple solution is going to a fully managed monitoring platform, in our case Cloudwatch. This way we could get rid of the burden that is the setup and management.

In this scenario, we thought of preparing some tooling to help the developers to setup their own alerts and dashboards, mainly with the help of **Terraform** and the **Python AWS SDK**. A great solution, one may think, but we found some issues, being **the big monthly costs** one of them.

Monitoring a fleet of 100 EC2 instances, to put an example, would cost around 30 Euros/month, alerts included. But the costs explode as soon as we want to use some metrics that don't exist out of the shelf. This is: disk utilization, memory usage, number of processes, Nginx metrics, application instrumentation, etc.

AWS charges you 0,30 Euros per custom metric, times the number of resources (Ec2 instances). Having an example of 5 custom metrics, this would be:

```
100 Ec2 instances x 5 metrics x 0.30 Eur/month = 150 Eur/month
```

It's clear that paying thousands of Euros every year for the monitoring alone cannot be justified. We have to search for alternatives.

Improving our current stack
---------------------------

Searching a bit in Google we found that Icinga has a plugin to import resources from [AWS](https://github.com/Icinga/icingaweb2-module-aws). This is: Ec2 instances, load balancers, RDS databases and auto scaling groups.

Keeping Iginga would be a good solution because we don't need to learn and setup a new platform and we know it's reliable. Alternatively, we could also use something like Grafana to generate dashboards with the metrics.

After playing around with a prototype I found several issues.

* I couldn't find an easy way to filter which resources I want to monitor. Something as simple as filtering by tag to only monitor the production resources. It may exist, because the importer configuration has a field for a filter expression but I found no documentation. As a result, the full inventory is imported.
* The plugin seems to be in an early stage of development and it's maintained by the community.
* Again, we cannot monitor things like containers. Probably it will be implemented over time.
* We cannot pull standard metrics from Cloudwatch. If we want to monitor an RDS database, we have to use a Nagios plugin.
* The import tasks need to be run periodically to keep the inventory current.
* The import works by autogenerating the same configuration files that we now maintain in our software repos and then reloading the Icinga configuration. Sometimes the imports fail because of syntax errors (self inflicted pain), causing the synchronization to fail. This would leave us blind if it's not spotted.

In general, it feels that the setup it's not appropriate for us. It would be a good solution for an organization that is using cloud services but, at the same time, is going to keep a quite static fleet. Also, not using hosted services at all.

What is the industry using?
---------------------------

We need:

* Monitor some static resources, like long running EC2 instances.
* Metrics from short living Ec2 instances in autoscaling groups.
* Perhaps some batch jobs that run for some hours and then the resources are destroyed.
* Hosted services like RDS and probably Kubernetes in the future.

What is the industry using to monitor such a diverse environment? It seems that all points to [Prometheus](https://prometheus.io).

Prometheus, like Munin, uses a pull model but it escalates better because it's written in Go and can auto-discover all the AWS services we are planning to use. Finally, for the graphing, it supports Grafana out of the box and the alerting capabilities are also fine for us (email, sms, webhooks, etc.).

Regarding the costs, it also seems to be a good solution, because it's open source and it doesn't have big hardware requirements nor we have to setup big database clusters. It also can easily run in a small Ec2 instance or in docker containers.

The only down side at the moment is the steep learning curve, because the platform is composed of many microservices, but it shouldn't be a big issue. We will try in the lab and some staging  environments but, after all the alternatives, it seems to be the right move.