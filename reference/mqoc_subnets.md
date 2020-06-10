---
copyright:
  years: 2020
lastupdated: "2020-06-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Queue manager subnets
{: #mqoc_subnets}

This section describes how to use the subnets listing for whitelisting queue managers.

## Subnets of a queue manager
{: #mqoc_subnets_qm}

Internally, IBM MQ on Cloud is deployed using a series of components that are built and deployed as containers into a Kubernetes cluster that runs in the particular geographical region you have selected. Each queue manager that you deploy will have an IP address associated with the worker node that it is currently deployed on.

It is not guaranteed that the IP address for a queue manager will stay the same over time. It may change because the queue manager has moved between worker nodes or has been moved as part of a disaster recovery procedure, for example. To mitigate this, you can set a subnet range as the whitelist for your queue managers which will cover all the known IP addresses that the queue manager could be assigned to.

The list of known current subnets is provided as a JSON file [here](http://ibm.biz/mqcloud-workerip) for ease of use programmatically. The list of subnets is arranged by region and domain. This file could be used to automatically upate any network configuration to apply whitelisting for all the known subnets that a queue manager could be using.
