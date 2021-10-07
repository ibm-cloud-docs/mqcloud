---
copyright:
  years: 2020, 2021
lastupdated: "2021-09-29"
---

{{site.data.keyword.attribute-definition-list}}

# Queue manager IP subnets
{: #mqoc_subnets}

This topic describes the IP subnets for queue manager network traffic in order to allow safe-listing of incoming queue manager traffic by customer-owned network firewalls.

## IP Subnets of a queue manager
{: #mqoc_subnets_qm}

In order to support scalability, high availability and disaster recovery scenarios {{site.data.keyword.mq_full}} runs on a flexible and dynamic set of infrastructure servers and so the IP address associated with a particular queue manager will change over time within a defined set of subnets for a particular geography.

To support users configuring network firewall rules in their on-premises or cloud environments we document the list of IP subnets for queue managers in each region at the following location;

- [Source IP subnets for {{site.data.keyword.mq_full}} queue managers](https://ibm.biz/mqcloud-workerip){: external}

We recommend to check the file for changes on a daily basis to avoid the risk of outages when the IP subnet ranges are updated.
