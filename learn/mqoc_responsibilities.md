---
copyright:
  years: 2021
lastupdated: "2021-08-26"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Your responsibilities with using IBM MQ on Cloud
{: #mqoc_responsibilities}

Learn about the responsibilities you have when you use IBM MQ on IBM Cloud. For overall terms of use, see [Cloud Services terms](https://cloud.ibm.com/docs/overview/terms-of-use?topic=overview-terms#terms).
{:shortdesc}

# Overview of shared responsibilities
{: #mqoc_responsibilities_overview}

IBM MQ on IBM Cloud is a managed service in the [IBM Cloud shared responsibility model](https://cloud.ibm.com/docs/overview/terms-of-use?topic=overview-shared-responsibilities). Review the following table of who is responsible for particular cloud resources when using IBM MQ on IBM Cloud. Then, you can view more granular tasks for shared responsibilities in Tasks for shared responsibilities by area.

| Resource | [Incident and operations management](#mqoc_incident_and_ops) | [Change management](#mqoc_change_management) | [Identity and access management](#mqoc_iam_responsibilities) | [Security and regulation compliance](#mqoc_security_compliance) | [Disaster Recovery](#mqoc_disaster_recovery) |
| - | - | - | - | - | - |
| [Data](#mqoc_applications_and_data) | You | You | You | You | You |
| [Applications](#mqoc_applications_and_data) | You | You | You | You | You |
| Observability | [Shared](#mqoc_incident_and_ops) | IBM | [Shared](#mqoc_iam_responsibilities) | IBM | IBM |
| Queue manager | [Shared](#mqoc_incident_and_ops) | [Shared](#mqoc_change_management) | [Shared](#mqoc_iam_responsibilities) | [Shared](#mqoc_security_compliance) | [Shared](#mqoc_disaster_recovery) |
| Certificates | [Shared](#mqoc_incident_and_ops) | IBM | IBM | IBM | IBM |
| App networking | IBM | IBM | IBM | IBM | IBM |
| Cluster networking | IBM | IBM | IBM | IBM | IBM |
| Cluster version | IBM | IBM | IBM | IBM | IBM |
| Worker nodes | IBM | IBM | IBM | IBM | IBM |
| Master | IBM | IBM | IBM | IBM | IBM |
| Service | IBM | IBM | IBM | IBM | IBM |
| Virtual storage | IBM | IBM | IBM | IBM | IBM |
| Virtual network | IBM | IBM | IBM | IBM | IBM |
| Hypervisor | IBM | IBM | IBM | IBM | IBM |
| Physical servers and memory | IBM | IBM | IBM | IBM | IBM |
| Physical storage | IBM | IBM | IBM | IBM | IBM |
| Physical network and devices | IBM | IBM | IBM | IBM | IBM |
| Facilities and Data Centers | IBM | IBM | IBM | IBM | IBM |

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column. The next five columns describe whether you, IBM, or both have shared responsibilities for a particular area."}
{: caption="Table 1. Responsibilities by resource." caption-side="top"}

## Tasks for shared responsibilities by area
{: #mqoc_task_responsibilities}

After reviewing the [overview](#mqoc_responsibilities_overview), see what tasks you and IBM share responsibility for each area and resource when you use IBM MQ on IBM Cloud.
{: shortdesc}

### Incident and operations management
{: #mqoc_incident_and_ops}

You and IBM share responsibilities for the set up and maintenance of your IBM MQ on IBM Cloud environment. You are responsible for incident and operations management of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Observability | <ul><li>Provide Log Analysis and Monitoring as managed add-ons to enable observability of your IBM MQ on IBM Cloud. Maintenance is simplified for you because IBM provides the installation and updates for the managed add-ons.</li><li>Provide integration with Activity Tracker and send IBM MQ on IBM Cloud API events for auditability.</li></ul> | <ul><li>[Set up and monitor the health](/docs/services/mqcloud?topic=mqcloud-logdna_logs) of your queue manager logs.</li><li>[Setup and monitor events in Activity Tracker](/docs/services/mqcloud?topic=mqcloud-at_events)</li></ul>|
| Queue manager | <ul><li>Provide a highly available queue manager deployment</li><li>Configure channels and queues for testing purposes</li><li>Monitoring of queue manager availability</li></ul> | <ul><li>Select the [queue manager size](/docs/services/mqcloud?topic=mqoc_qm_sizes) based on messaging requirements</li><li>Monitor [IBM Cloud status](https://cloud.ibm.com/status/maintenance?component=mqcloud) for planned maintenance</li><li>Configuring and monitoring queue depth to ensure storage requirements do not exceed limits</li><li>Monitoring open connections to ensure they do need exceed limits</li><li>Configure multiple queue managers in different regions to provide additional [high availability](/docs/services/mqcloud?topic=mqoc_ha)</li></ul>|
| Certificates | <ul><li>Provide Let's Encrypt signed certificates</li><li>Refresh provided certificates before expiry</li></ul> | <ul><li>Optionally: [Import user defined certificate chains](/docs/services/mqcloud?topic=mqoc_qm_certs)</li><li>Ensure that user provided certificates do not expire</li><li>Configure certificate usage on queue manager channels</li></ul>|

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 2. Responsibilities for incident and operations management" caption-side="top"}


### Change Management
{: #mqoc_change_management}

You and IBM share responsibilities for managing queue manager changes in the IBM MQ on IBM Cloud environment. You are responsible for change management of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Queue manager | <ul><li>Automatic upgrade to the latest revision</li></ul> | <ul><li>Managing queue manager configuration</li><li>Optional: manually upgrade queue managers to the latest revision before automatic upgrade</li></ul> |

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 3. Responsibilities for change management" caption-side="top"}

### Identity and access management
{: #mqoc_iam_responsibilities}

You and IBM share responsibilities for controlling access to the IBM MQ on IBM Cloud environment. You are responsible for identity and access management of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Observability | <ul><li>Provide the ability to integrate IBM Cloud Activity Tracker to audit the actions that users take in IBM MQ on IBM Cloud.</li></ul> | <ul><li>Set up IBM Cloud Activity Tracker or other capabilities to track user activity.</li></ul> |
| Queue Manager | <ul><li>Configure specified IBM Cloud users and applications with the required IAM policies</li><li>Provide API keys for user and applications to authenticate</li></ul> | <ul><li>Define the users and applications that have access to queue managers</li><li>Configure authority records for queue manager specific resources</li></ul>|

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 4. Responsibilities for identity and access management" caption-side="top"}

### Security and regulation compliance
{: #mqoc_security_compliance}

IBM is responsible for the security and compliance of the IBM MQ on IBM Cloud service.  You and IBM share responsibilities for the security and compliance of the queue managers. You are responsible for security and regulation compliance of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Queue Manager | <ul><li>Maintain controls to meet industry compliance standards such as ISO27k</li><li>Provide default queue manager resources that are TLS enabled</li><li>Monitor, isolate, and recover the queue manager</li><li>Automatically apply security patch updates</li><li>Disable certain insecure actions such as channel exits</li><li>Continuously monitor queue manager images to detect vulnerability and security compliance issues</li></ul> | <ul><li>Configure queue manager security such as TLS and AMS on queue manager resources</li><li>Configure authority records for queue manager resources to limit access to only required users and applications</li></ul> |

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 5. Responsibilities for security compliance" caption-side="top"}

### Disaster recovery
{: #mqoc_disaster_recovery}

You and IBM share responsibilities for the set up and maintenance of your IBM MQ on IBM Cloud environment. You are responsible for disaster recovery of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Queue Manager | <ul><li>Backup queue manager configuration daily</li><li>Recover required infrastructure</li><li>Provision new infrastructure in a backup availability zone, if recovery is not possible</li><li>Redeploy queue managers to new availability zone</li><li>Restore queue manager configuration from previous backup</li></ul> | <ul><li>[Register for disaster recovery notifications](/docs/services/mqcloud?topic=mqcloud-mqoc_dr_notifications)</li><li>Reset channel sequence numbers so that channels will successfully communicate</li></ul> |

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 6. Responsibilities for disaster recovery" caption-side="top"}

### Applications and data
{: #mqoc_applications_and_data}

You are completely responsible for the applications and data that you use with IBM MQ on IBM Cloud . However, IBM provides various tools to help you set up, manage, secure, integrate and optimize your apps as described in the following table.
{: shortdesc}

| Resource | How IBM helps | What you can do |
| -------- | -------------------- | --------------------- |
| Applications | <ul><li>Provide default queue manager configuration to allow applications to connect securely</li><li>Provide sample applications such as [MQ JMS client](https://developer.ibm.com/messaging/learn-mq/mq-tutorials/develop-mq-jms/)</li><li>Generate an API key that is used to access queue managers</li><li>Provide application connection configuration in JSON CCDT format</li></ul> | <ul><li>Maintain responsibility for your apps, data, and their complete lifecycle</li><li>Configure applications for [high availability](/docs/services/mqcloud?topic=mqoc_ha)<li>Manage open connections to ensure the maximum queue manager limit is not exceeded</li></ul> |
| Data | <ul><li>Provide encrypted persistent storage for persistent messages </li><li>Separation of storage from queue manager runtime allowing queue managers to recover within an availablity zone with no data loss</ul> | <ul><li>Maintain responsibility for your data and how your apps consume the data</li><li>Control queue sizes to prevent storage limits being exceeded</li><li>Encrypt message payload in transit and at rest using Advanced Message Security (AMS)</ul> |

{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 7. Applications and data" caption-side="top"}