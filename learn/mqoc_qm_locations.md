---
copyright:
  years: 2018, 2023
lastupdated: "2023-05-17"
---

{{site.data.keyword.attribute-definition-list}}

# Deployment locations
{: #deploy_locations}

{{site.data.keyword.mq_full}} provides a managed service that allows queue managers to be deployed to both {{site.data.keyword.cloud_notm}} and Amazon Web Services (AWS).
{: shortdesc}

## Queue manager locations
{: #deploy_qm_locations}

The location of a service instance is selected from a dropdown list when creating the service instance.

The list of queue manager locations available depends on where the service instance was created. This list is displayed in the queue manager creation page, as shown below.

![Image showing queue manager locations](../images/mqoc_qm_locations.png)

Queue managers can be deployed to IBM Cloud or Amazon Web Services by selecting the preferred location from the drop down list.

Service instance location         | Queue manager deployment locations
----------------------------------|--------------
`Dallas (us-south)`               | `IBM Cloud US South (Dallas)`  \n`AWS US East 1 (North Virginia)`
`Frankfurt (eu-de)`               | `IBM Cloud Germany (Frankfurt)`  \n`AWS EU West 1 (Ireland)`
`London (eu-gb)`                  | `IBM Cloud United Kingdom (London)`
`Washington DC (us-east)`         | `IBM Cloud US East`

Lite queue managers are only available in IBM Cloud locations. Other sizes are available in all locations.

Choose the cloud location which is geographically closest to your position -  this will help to lower latency and give optimal performance. Please contact us if you would like to discuss additional deployment locations.
{: tip}

The location of a deployed queue manager can be found by examining the queue manager details page:

![Image showing queue manager locations](../images/mqoc_qm_locations_qminfo.png)

Amazon Web Services and AWS are trademarks of Amazon.com, Inc. or its affiliates in the United States and/or other countries.
{: note}
