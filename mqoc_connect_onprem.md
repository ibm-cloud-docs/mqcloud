---
copyright:
  years: 2017, 2021
lastupdated: "2021-09-28"

subcollection: mqcloud

keywords: connect, onprem, secure gateway, direct, internet, pass-thru
---

{{site.data.keyword.attribute-definition-list}}

# Overview of on-premises connection methods
{: #mqoc_connect_onprem}

There are several possible ways of connecting a cloud queue manager to an existing or new on-premises queue manager - the right choice for you will depend on your network topology and security requirements.

The two methods explained here are:

* [Connecting the queue managers directly](#mqoc_connect_onprem_direct_sect)
* [Connecting via IBM Cloud Secure Gateway](#mqoc_connect_onprem_gateway_sect)

A third method using passthru is noted here:

* [Connecting via IBM MQ Internet Pass-Thru](#mqoc_connect_onprem_passthru_sect)

The following sections provide information to assist you in deciding which option is the best for you. Each section contains a link to more detailed guidance and information about the configuration required.

## Direct connection initiated by the on-premises queue manager
{: #mqoc_connect_onprem_direct_sect}

This configuration works in the case where the on-premises queue manager can make calls out to the cloud queue manager but has no publicly visible IP address and cannot be directly addressed by incoming internet applications attempting to make a connection.

This is the simplest option to configure. For on-premise to cloud communication is uses a simple sender/receiver channel pair and for cloud to on-premise communication it uses a requester/server channel pair to establish the connection from the on-premises queue manager to the cloud queue manager.

Because the cloud queue manager cannot initiate the connection in this configuration, it is the on-premises queue manager which reaches out to the cloud queue manager to establish the connection. This method establishes a pair of channels and enables bi-directional flow of messages over the pair of channels.

The [guidance on direct connection](/docs/mqcloud?topic=mqcloud-mqoc_connect_onprem_direct) will help you implement this solution.

![Direct Connection][./images/mqoc_connect_onprem1.png]

## Connection via the IBM Cloud Secure Gateway
{: #mqoc_connect_onprem_gateway_sect}

The IBM Cloud Secure Gateway is a service built into IBM Cloud which facilitates connectivity between cloud and on-premises services.

The gateway is particularly useful in configurations where the on-premises queue manager is in a part
of the network which has no direct outbound connectivity. The secure gateway client is installed in a
customer network location which does have outbound IP traffic access. The gateway client carries traffic securely
from the on-premises queue manager via the gateway server to the cloud queue manager, and vice-versa.

Once the Secure Gateway connection has been established MQ channels can be initiated from either the cloud or the on-premise side, enabling a wider set of MQ channel types..

Similar to direct connection, this solution supports end-to-end TLS sessions between the on-premises queue manager and cloud-based queue manager.

The [guidance on secure gateway connection](/docs/mqcloud?topic=mqcloud-mqoc_connect_onprem_gateway) will help you implement this solution.

![IBM Secure Gateway][./images/mqoc_connect_onprem2.png]

## Connection via IBM MQ Internet Pass-thru
{: #mqoc_connect_onprem_passthru_sect}

Existing users of MQ Internet Pass-Thru will be familiar with this method of connectivity using HTTPS ( and particularly HTTPS tunnelling). A detailed overview of this approach is available at [MQ IPT Knowledge Base](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_latest/com.ibm.mq.ipt.doc/ipt0000_.htm){: external}.

This method may be most suitable for communication which must pass through a standard firewall configuration, and HTTP/HTTPS traffic is the most appropriate.

![MQ Internet PassThru][./images/mqoc_connect_onprem3.png]
