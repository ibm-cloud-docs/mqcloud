---
copyright:
  years: 2018, 2019
lastupdated: "2019-02-04"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Queue manager locations
{: #mqoc_qm_locations}

In this section, you can learn about the locations to which you can deploy queue managers for IBM MQ on Cloud.

{:shortdesc}

## Queue manager locations

The location of a service instance is selected from a dropdown list when creating the service instance.

The list of queue manager locations available depends on where the service instance was created. This list is displayed in the queue manager creation page, as shown below.

<img src="../images/mqoc_qm_locations.png" alt="Image showing queue manager locations" style="width:400px;"/>

Queue managers can be deployed to IBM Cloud or Amazon Web Services by selecting the preferred location from the drop down list.

The full list of available locations is:

For instances created in the EU-GB location:

* IBM Cloud EU-GB (London)

For instances created in the EU-DE location:

* IBM Cloud EU-DE (Frankfurt)

For instances created in the US South location:

* IBM Cloud US South (Dallas)
* AWS US East 1 (North Virginia)

Lite queue managers are only available in IBM Cloud locations. Other sizes are available in all locations.

We recommend that you choose the cloud location which is geographically closest to your position -  this will help to lower latency and give optimal performance. Please contact us if you would like to discuss additional deployment locations.

The location of a deployed queue manager can be found by examining the queue manager details page:

<img src="../images/mqoc_qm_locations_qminfo.png" alt="Image showing queue manager locations" style="width:400px;"/>

## Note:

Amazon Web Services and AWS are trademarks of Amazon.com, Inc. or its affiliates in the United States and/or other countries.
