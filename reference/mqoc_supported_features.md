---
copyright:
  years: 2020
lastupdated: "2020-01-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM MQ supported features
{: #mqoc_supported_features}

This section describes IBM MQ features that are supported by IBM MQ on Cloud queue managers.

 - MQ Clients including Java, JMS, C, C++, .NET, XMS, COBOL, Node.js and Golang
 - IBM MQ Bridge to Salesforce integration (bridge component must be deployed separately by the customer)
 - IBM MQ Bridge to Blockchain integration (bridge component must be deployed separately by the customer)
 - IBM MQ Internet Pass-Thru (MQIPT) (MQIPT component must be deployed separately by the customer)
 - Secure Gateway Service (provisioned separately through IBM Cloud)
 - IBM MQ Advanced Message Security (AMS)
 - IBM MQ Managed File Transfer (MFT)
 - IBM MQ REST Messaging APIs (for sending a receiving messages)
 - IBM MQ REST Administrative APIs (for configuring the queue manager)
 - IBM MQ clustering (clusters can include a mix of IBM MQ on Cloud queue managers and privately deployed queue managers)

<br/>

## IBM MQ features not currently supported
{: #mqoc_unsupported_features}

This section describes IBM MQ features that are not currently supported by IBM MQ on Cloud queue managers.

 - Advanced Message Queuing Protocol (AMQP)
 - MQ Telemetry Transport (MQTT)
 - Channel Exits, Service definitions, Process definitions - for security reasons we do not support the injection of arbitrary custom code
 - Self-service configuration updates to qm.ini - please raise a cloud support ticket if you wish to discuss a request to configure an item in the qm.ini
 - Replicated data queue managers (RDQM) - internal deployment architecture and high availability model is owned by IBM
