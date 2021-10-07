---
copyright:
  years: 2020, 2021
lastupdated: "2021-09-29"
---

{{site.data.keyword.attribute-definition-list}}

# IBM MQ supported features
{: #mqoc_supported_features}

This section describes IBM MQ features that are supported by {{site.data.keyword.mq_full}} queue managers.
{: shortdesc}

- MQ Clients including Java, JMS, C, C++, .NET, XMS, COBOL
- IBM MQ Bridge to Salesforce integration (bridge component must be deployed separately by the customer)
- IBM MQ Bridge to Blockchain integration (bridge component must be deployed separately by the customer)
- IBM MQ Internet Pass-Thru (MQIPT) (MQIPT component must be deployed separately by the customer)
- Secure Gateway Service (provisioned separately through IBM Cloud)
- IBM MQ Advanced Message Security (AMS)
- IBM MQ Managed File Transfer (MFT)
- IBM MQ REST Messaging APIs (for sending a receiving messages)
- IBM MQ REST Administrative APIs (for configuring the queue manager)
- IBM MQ clustering (clusters can include a mix of {{site.data.keyword.mq_full}} queue managers and privately deployed queue managers)

## IBM MQ permitted features
{: #mqoc_permitted_features}

This section describes IBM MQ features that are permitted by {{site.data.keyword.mq_full}} queue managers but are only supported via the open-source GitHub.com community.

- MQ Clients using Node.js
- MQ Clients using Golang

## IBM MQ features not currently supported
{: #mqoc_unsupported_features}

This section describes IBM MQ features that are not currently supported by {{site.data.keyword.mq_full}} queue managers.

- Advanced Message Queuing Protocol (AMQP)
- MQ Telemetry Transport (MQTT)
- Channel Exits, Service definitions, Process definitions - for security reasons we do not support the injection of custom code
- Self-service configuration updates to qm.ini - please raise a cloud support ticket if you wish to discuss a request to configure an item in the qm.ini
- Replicated data queue managers (RDQM) - internal deployment architecture and high availability model is owned by IBM
