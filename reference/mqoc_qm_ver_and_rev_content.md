---
copyright:
  years: 2018, 2019
lastupdated: "2018-08-06"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Queue manager update content by version and revision
{: #index}

In this section, you can read about IBM queue manager updates by version and revision for MQ on IBM Cloud.

{:shortdesc}

## 9.1.1 r2
### Available from 5th February 2019
{: #mqoc_qm_9.1.1r2}
* Required security and vulnerability fixes.
* Reduced queue manager deploy time.
* Improved resilience and performance when authenticating clients.

## 9.1.1 r1
### Available from 2nd January 2019 to 5th March 2019
{: #mqoc_qm_9.1.1r1}
* Update to MQ version 9.1.1
* For more information see [What's new in MQ 9.1.1](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.1.0/com.ibm.mq.pro.doc/q132240_.htm)

## 9.1.0 r2
### Available from 9th August 2018 to 6th February 2019
{: #mqoc_qm_9.1.0r2}
* Required security and vulnerability fixes.
* Enable the ability to set up certificates on queue managers so that TLS and AMS can be configured.

## 9.1.0 r1
### Available from 20th July 2018 to 11th September 2018
{: #mqoc_qm_9.1.0r1}
* Update to MQ version 9.1.0
* For more information see [What's new in MQ 9.1](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.1.0/com.ibm.mq.pro.doc/q113110_.htm)
* **Note on the release model for IBM MQ on Cloud:**
  * The MQ on Cloud service follows the "Continuous Delivery" (CD) model which means that all queue managers (including those deployed on MQ v9.1.0) will be upgraded to the next CD version within a defined period of time after the next CD version becomes available.
  * In particular the MQ on Cloud service treats MQ v9.1.0 as a CD version and not a "Long Term Support" (LTS) version.

## 9.0.5 r2
### Available from 4th July 2018 to 21st August 2018
{: #mqoc_qm_9.0.5r2}
* Required security and vulnerability fixes.
* Enable use of the messaging REST API (see [Using the messaging REST API](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.dev.doc/q130940_.html) for more details).
* Automated restart of MQ Web Console process in the event of a failure.
* Enhance the naming format of the diagnostic logs download file to make the queue manager and timezone obvious to enable the file to be more useful once it has been downloaded - e.g. log_QM1_010518_0927Z.zip.
* Tuning of queue manager log files to increase message throughput.
* Ensure that expired logs and diagnostic files, collected from the IBM Cloud user interface, are deleted after 7 days.
* MQ Web Console configuration updates to the default view (title changed and reordering of widgets).
* Improved performance when querying the queue manager status from the IBM Cloud user interface.
* Ability to trigger the starting of a channel when a message arrives on the transmit queue.
