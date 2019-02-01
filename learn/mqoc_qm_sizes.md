---
copyright:
  years: 2018
lastupdated: "2018-03-12"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Queue manager sizes
{: #index}

Learn about the characteristics of IBM queue managers available to deploy on IBM Cloud.

{:shortdesc}

## Lite queue managers

To give you a taste of MQ as a managed service, the MQ on IBM Cloud service offers a Lite queue manager. If you do not currently have a Lite queue manager deployed, you can create one by following the [creating a queue manager](../mqoc_create_qm.html) guide.

Note:
* You can only deploy one Lite queue manager per Lite service instance
* You can delete an existing Lite queue manager and deploy a new one at any time
* Lite queue managers will automatically be deleted after 30 days of inactivity but you are welcome to deploy a new one
* You will never be charged for a Lite queue manager

## Billable queue managers

The MQ on IBM Cloud service offers the following billable queue manager sizes:
* **Small**: Appropriate for light workloads such as supporting an individual department or application

* **Medium**: Appropriate for shared use by a number of light to moderate workload applications

* **Large**: Appropriate for heavy throughput scenarios where transaction performance is critical

A billable queue manager is charged based on the number of Virtual Processor Core (VPC) hours that it is active - for example, a Medium size queue manager is charged at four times (4x) the rate of a Small size queue manager. The hourly cost is dependent on your local currency and can be seen in the Pricing Plan at the bottom of the [MQ service catalog page](https://console.bluemix.net/catalog/services/mq), where you can select your country or region.

You can see details of your billable usage in the [IBM Cloud usage dashboard](https://console.bluemix.net/account/usage) at the Account or Resource Group level.

**Note**: if you cannot see your MQ usage on the dashboard, but have deployed a billable queue manager, ensure you have selected to view the usage for your resource group, e.g. Under the Usage Dashboard title, in the `Group:` dropdown menu, select `Resource Groups` then `default`.

## Queue manager resources

The following table provides information about the resources available to each queue manager size and performance results based on testing:

|                               | Lite    | Small | Medium | Large |
|-------------------------------|---------|-------|--------|-------|
| VPC                           | Up to 1 | 1     | 4      | 12    |
| Memory (RAM GB)               | 1       | 1     | 4      | 8     |
| Disk Size (GB)                | 10      | 20    | 40     | 100   |
| Disk performance (IO operations per second - IOPS) | 40      | 200   | 400    | 1000  |
| Maximum concurrent client connections<sup id="a1">[ 1](#f1)</sup> | 20      | 50    | 200    | 1000  |

---

_<b id="f1">1.</b> The IBM MQ JMS client library typically uses two client connections per application (one for the JMS Connection and one for each JMS Session) so a connection limit of 20 supports up to 10 concurrent JMS applications._

_<b id="f2">2.</b> Overall throughput is based on the maximum number of client connections being used to actively produce and consume messages. Throughput for single connection client applications may be lower.
Throughput measurements are based on producing and consuming applications deployed in the same IBM Cloud data centre. Observed throughput for applications running in remote locations may be lower due to network latency between the client and the cloud queue manager._
