---
copyright:
  years: 2018, 2023
lastupdated: "2023-05-17"
---

{{site.data.keyword.attribute-definition-list}}

# Deployment Locations
{: #deploy_locations}

{{site.data.keyword.mq_full}} provides a managed service that allows queue managers to be deployed to both {{site.data.keyword.cloud_notm}} and Amazon Web Services (AWS).
{: shortdesc}

## Reserved Instance Plan Locations
{: #deploy_ri_locations}

Service instance location         | Plans Available                    | Queue manager deployment locations
----------------------------------|------------------------------------|-------------------------
`London (eu-gb)`                  | `Reserved Capacity Subscription` \n `Reserved Deployment` | `IBM Cloud United Kingdom (London)`
`Washington DC (us-east)`         | `Reserved Capacity Subscription` \n `Reserved Deployment` | `IBM Cloud US East (Washington DC)`

## Multi Tenant Plan Locations
{: #deploy_mt_locations}

Service instance location         | Plans Available                    | Queue manager deployment locations
----------------------------------|------------------------------------|-------------------------
`Dallas (us-south)`               | `Custom Enterprise` \n `Default` \n `Lite`   | `IBM Cloud US South (Dallas)`  \n`AWS US East 1 (North Virginia)`
`Frankfurt (eu-de)`               | `Custom Enterprise` \n `Default` \n `Lite`   | `IBM Cloud Germany (Frankfurt)`  \n`AWS EU West 1 (Ireland)`
`London (eu-gb)`                  | `Custom Enterprise` \n `Default` \n `Lite`  | `IBM Cloud United Kingdom (London)`
`Washington DC (us-east)`         | `Custom Enterprise` \n `Default`             | `IBM Cloud US East (Washington DC)`

## Queue Manager Locations
{: #deploy_qm_locations}

The list of queue manager locations available depends on the plan type and location selected when the service instance was created. This list is displayed in the queue manager creation page, as shown below.

![Image showing queue manager locations](../images/mqoc_qm_locations.png)

Lite queue managers are only available for multi tenant plan types in IBM Cloud locations. Other sizes are available in all locations.

Choose the cloud location which is geographically closest to your position -  this will help to lower latency and give optimal performance. Please contact us if you would like to discuss additional deployment locations.
{: tip}

The location of a deployed queue manager can be found by examining the queue manager details page:

![Image showing queue manager locations](../images/mqoc_qm_locations_qminfo.png)

Amazon Web Services and AWS are trademarks of Amazon.com, Inc. or its affiliates in the United States and/or other countries.
{: note}
