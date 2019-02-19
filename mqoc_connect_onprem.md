---
copyright:
  years: 2017, 2019
lastupdated: "2018-05-02"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{: #mqoc_connect_onprem}
# Overview of on-premises connection methods


There are several possible ways of connecting a cloud queue manager to an existing or new on-premises queue manager - the right choice for you will depend on your network topology and security requirements.

The three methods explained here are:

* [Connecting the queue managers directly](#mqoc_connect_onprem_direct)
* [Connecting via IBM Cloud Secure Gateway](#mqoc_connect_onprem_gateway)
* [Connecting via IBM MQ Internet Pass-Thru](#mqoc_connect_onprem_passthru)

The following sections provide information to assist you in deciding which option is the best for you. Each section contains a link to more detailed guidance and information about the configuration required.

---

{: #mqoc_connect_onprem_direct}
## Direct connection initiated by the on-premises queue manager


This configuration works in the case where the on-premises queue manager can make calls out to the cloud queue manager but has no publicly visible IP address and cannot be directly addressed by incoming internet applications attempting to make a connection.

This is the simplest option to configure. For on-premise to cloud communication is uses a simple sender/receiver channel pair and for cloud to on-premise communication it uses a requester/server channel pair to establish the connection from the on-premises queue manager to the cloud queue manager.

Because the cloud queue manager cannot initiate the connection in this configuration, it is the on-premises queue manager which reaches out to the cloud queue manager to establish the connection. This method establishes a pair of channels and enables bi-directional flow of messages over the pair of channels.

The [guidance on direct connection](/docs/services/mqcloud/mqoc_connect_onprem_direct.html) will help you implement this solution.

![alt text][connect_on_prem1]

[connect_on_prem1]: ./images/mqoc_connect_onprem1.png "Direct Connection"

---

{: #mqoc_connect_onprem_gateway}
## Connection via the IBM Cloud Secure Gateway


The IBM Cloud Secure Gateway is a service built into IBM Cloud which facilitates connectivity between cloud and on-premises services.

The gateway is particularly useful in configurations where the on-premises queue manager is in a part
of the network which has no direct outbound connectivity. The secure gateway client is installed in a
customer network location which does have outbound IP traffic access. The gateway client carries traffic securely
from the on-premises queue manager via the gateway server to the cloud queue manager, and vice-versa.

Once the Secure Gateway connection has been established MQ channels can be initiated from either the cloud or the on-premise side, enabling a wider set of MQ channel types..

Similar to direct connection, this solution supports end-to-end TLS sessions between the on-premises queue manager and cloud-based queue manager.

The [guidance on secure gateway connection](/docs/services/mqcloud/mqoc_connect_onprem_gateway.html) will help you implement this solution.

![alt text][connect_on_prem2]

[connect_on_prem2]: ./images/mqoc_connect_onprem2.png "IBM Secure Gateway"

---

{: #mqoc_connect_onprem_passthru}
## Connection via IBM MQ Internet Pass-thru


Existing users of MQ Internet Pass-Thru will be familiar with this method of connectivity using HTTPS ( and particularly HTTPS tunnelling). A more detailed overview of this approach is available at [MQ IPT  Knowledge Base ](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.ipt.doc/ipt0000_.htm).

This method may be most suitable for communication which must pass through a standard firewall configuration, and HTTP/HTTPS traffic is the most appropriate.

![alt text][connect_on_prem3]

[connect_on_prem3]: ./images/mqoc_connect_onprem3.png "MQ Internet Passthru"
