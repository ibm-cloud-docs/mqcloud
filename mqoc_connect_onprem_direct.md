---
copyright:
  years: 2017, 2019
lastupdated: "2018-05-02"

subcollection: mqcloud

keywords: connect, onprem, direct
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Direct connection to an on-premises queue manager
{: #mqoc_connect_onprem_direct}

In order to directly connect an IBM MQ On Cloud queue manager to an on-premises queue manager there are several steps to follow.

* Create the queues in the MQ On Cloud queue manager.

  * A remote queue to hold messages from the cloud application connected to a transmit queue.
  * A local queue to hold responses from the on-premises queue manager requester channel.


* Create the channels and authorizations to allow the MQ On Cloud queue manager to connect.

  * The server channel - this channel will receive the initial connection from the on-premises queue manager, and will forward the messages from the transmit queue.
  * A receiver channel - this channel will receive responses from the on-premises sender channel.


* Create the queues in the on-premises queue manager.

  * A local queue - this queue will hold messages destined for the on-premises application
  * A remote queue - this queue is connected to a transmit queue to hold responses from the on-premises application
  destined for the cloud queue manager.


* Create the channels and authorizations to connect to the MQ On Cloud queue manager.

  * A requester channel - this channel corresponds to the server channel on the cloud - connected to the local queue.
  * A sender channel - this channel corresponds to the receiver channel on the cloud queue manager - accepting
  messages from the transmit queue and forwarding them to the cloud queue manager.


* Set up TLS security by giving the local queue manager the certificates to permit a trust relationship between the two queue managers.

[Download full instructions here](https://ibm.biz/BdqDUD) in PDF format.

![alt text][connect_on_prem1]

[connect_on_prem1]: ./images/mqoc_connect_onprem1.png "Direct Connection"

{:shortdesc}
