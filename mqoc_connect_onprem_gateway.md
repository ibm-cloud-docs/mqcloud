---
copyright:
  years: 2017, 2020
lastupdated: "2018-05-03"

subcollection: mqcloud

keywords: connect, onprem, secure gateway
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting to on-premises queue manager using IBM Cloud Secure Gateway
{: #mqoc_connect_onprem_gateway}

In order to connect an IBM MQ On Cloud queue manager to an on-premises queue manager via the IBM Secure Gateway there are several steps to follow:

1. Create an MQ cloud queue manager (or use an existing one).
2. Create an on-premises MQ queue manager (or use an existing one).
3. Create a cloud based IBM Secure Gateway, install its client on-premises and configure the Secure Gateway to link the two Queue Managers.
4. Create channels to pass messages between the two Queue Managers.
5. Set up TLS security by giving the local queue manager the certificates to permit a trust relationship between the two queue managers.

[Download full instructions here](http://ibm.biz/BdqDUx) in PDF format.

![alt text][connect_on_prem2]

[connect_on_prem2]: ./images/mqoc_connect_onprem2.png "IBM Secure Gateway"
