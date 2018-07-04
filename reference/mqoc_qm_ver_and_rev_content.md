---
copyright:
  years: 2018
lastupdated: "2018-07-02"
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

## 9.0.5 r2
{: #mqoc_qm_9.0.5r2}
1. Required security and vulnerability fixes.
2. Enable use of the messaging REST API (see [Using the messaging REST API](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.dev.doc/q130940_.html) for more details).
3. Automated restart of MQ Web Console process in the event of a failure.
4. Enhance the naming format of the diagnostic logs download file to make the queue manager and timezone obvious to enable the file to be more useful once it has been downloaded - e.g. log_QM1_010518_0927Z.zip.
5. Tuning of queue manager log files to increase message throughput.
6. Ensure that expired logs and diagnostic files, collected from the IBM Cloud user interface, are deleted after 7 days.
7. MQ Web Console configuration updates to the default view (title changed and reordering of widgets).
8. Improved performance when querying the queue manager status from the IBM Cloud user interface.
9. Ability to trigger the starting of a channel when a message arrives on the transmit queue.
