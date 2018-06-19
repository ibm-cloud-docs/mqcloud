---
copyright:
  years: 2018
lastupdated: "2018-04-25"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Queue manager versions
{: #index}

In this section, you can learn about the IBM queue manager versions and revisions for MQ on IBM Cloud.

{:shortdesc}

## Queue manager details

![Image showing queue manager details](../images/mqoc_qm_details.png)

The queue manager *Configuration* tab shows details about the current queue manager, including the MQ version, revision, and the date it was last updated. Hovering over the information icons reveals additional detail, such as the build level and the time of the last update.

### MQ version

The version and maintenance level of the queue manager for example, 9.0.5, represents the fifth Continuous Delivery (CD) release within the v9.0 family.

From time to time new versions of the MQ product will be released, such as during a new Continuous Delivery (CD) release. The new version of MQ will automatically become the default selection for new queue manager deployments, and existing queue managers will be notified that they have a specified time window in order to upgrade to the latest version.

### MQ build level

Hovering over the information icon next to the *MQ version* field reveals the build level. The build level includes the date that the MQ level was built, which changes when a fix has been applied to the queue manager deployment.

![Image showing queue manager build number](../images/mqoc_qm_build_level.png)

### Revision

The MQ on IBM Cloud service uses the term "revision" to describe different levels of the container image that runs inside an individual queue manager. Revisions are a sub-division within the MQ version. For example, the operating system image used in "9.0.4 r1" is not generally the same as "9.0.5 r1". Revisions are inclusive so "9.0.5 r3" would contain the changes in "9.0.5 r1" and "9.0.5 r2".

Periodically, a new revision will be released for a given MQ version. The new revision will automatically become the default selection for new queue manager deployments, and existing queue managers will be notified that they have a specified time window in order to upgrade to the latest revision. The length of the time window depends on the severity of the fixes contained in the new revision. A high severity security fix would need to be applied more quickly than a low severity fix.

A new revision may include one or more of the following:
* Applied queue manager fixes, such as required security fixes
* New or updated operating system dependencies
* Fixes or new features specific to the MQ on Cloud service

### Last updated

The date that is stated is when the queue manager was deployed. Following this, the date represents when it was most recently updated to a new version or revision.

![Image showing queue manager build number](../images/mqoc_qm_updated_time.png)

Hovering over the information icon next to the *Last updated* field reveals the time of day of the last update .
