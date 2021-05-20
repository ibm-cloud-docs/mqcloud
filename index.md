---
copyright:
  years: 2017, 2020
lastupdated: "2019-02-04"

subcollection: mqcloud

keywords: introduction, why, learn
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduction to IBM MQ
{: #mqoc_new_to_mq}

<img style="padding: 0 15px; float: left;" src="./images/MQ_Light_Icon@4x.png?raw=true" alt="Image of MQ Logo"/>
IBM MQ is an enterprise grade messaging middleware service that gives independent and potentially non-concurrent applications secure messaging capabilities, such as point-to-point and publish/subscribe models. MQ has been proving itself as an effective messaging solution for more than 25 years. This IBM MQ on Cloud service enables you to use IBM MQ as a managed offering, therefore IBM will handle upgrades, patches and also many of the operational management tasks, allowing you to focus on the integration of MQ with your applications.
In addition to the cloud service, IBM MQ is available in a wide range of customer-managed deployment form factors such as software for many operating systems including Linux and Windows. It is available as a containerised application and within a Kubernetes cluster, it is even available as something known as the MQ appliance which is dedicated hardware for running MQ. It is also available on the IBM z/OS mainframe.

The managed service, which is available in both {{site.data.keyword.cloud_notm}} and Amazon Web Services (AWS) removes much of the responsibility of running and maintaining an MQ environment.  These responsibilities include:
 - Operating System Patching
 - IBM MQ patching
 - IBM MQ upgrades
 - Availability
 - Failover

![Image showing IBM Cloud](./images/ibmcloudlogo.png) and also ![Image showing powered by AWS](./images/PB_AWS_logo_RGB.jpg)

## Why would I use MQ

When someone builds a network to process thousands of transactions every minute, one needs to ensure that not even a single transaction is lost. If the servers are unable to process the number of transactions fast enough it is highly likely that transactions may be lost. MQ works by storing the transactions to be processed on a message queue and then processing them one at a time. This allows transactions to be processed at a flat rate meaning that extra CPU during high demand times is not required. It also means that if the system were to suddenly break down, the messages that are being processed are safely stored on the message queue and will not be lost.

IBM MQ integrates with many different operating systems and languages such as Java, Node.js and Golang, and includes REST API capabilities that can be called from any programming or scripting language. MQ carries out all necessary data transformations for you. Once MQ is integrated on your system you no longer need to worry about the complexities of securely transforming and sending a message as MQ carries out all of this for you including encryption and decryption.

Learn how IBM MQ is different to other messaging solutions and other frequently asked questions here: https://www.ibm.com/products/mq/faq

## Learn MQ

IBM MQ is the most powerful messaging solution available on the market, it enables applications to communicate and share data with one another, it is highly scaleable and can be applied to a wide range of business needs, learn how IBM MQ can benefit your application scenario here: https://developer.ibm.com/components/ibm-mq/articles/mq-fundamentals

You can try MQ for free and without the need for any expensive infrastructure costs by creating a lite queue manager in IBM Cloud. MQ on Cloud has been developed with ease of use in mind and requires no specialist knowledge to use. You can find instructions on how to deploy a queue manager in IBM Cloud here:  https://developer.ibm.com/tutorials/mq-connect-app-queue-manager-cloud/

Interested in proving your knowledge? Become an MQ expert and prove your knowledge with the official IBM MQ developer badge, you will be able to work your way through some tutorials and learn all MQ fundamentals as well as some more in depth knowledge of creating applications that can utilise MQ to communicate: https://developer.ibm.com/components/ibm-mq/series/badge-ibm-mq-developer-essentials

## Administering an MQ on Cloud queue manager

MQ on Cloud allows you to use all of the traditional MQ administration tools, including a web based version of the MQ Console. You can find instructions on how to use the console here: 
https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_admin_mqweb

MQ on Cloud can be administered via locally installed tools too. MQ Explorer is a locally installed Eclipse-based tool for administering IBM MQ which you can install on a machine of your choosing, it connects to MQ on Cloud using a client connection and is supported on both Windows and Linux based environments.
You can also use the runmqsc Command Line Interface to administer MQ on Cloud queue managers. The CLI enables the ability to create scripts containing groups of MQ commands so that many different tasks can be carried out at the same time. It can be installed as part of the MQ clients bundle and is available on Windows and Linux. You can learn more about using MQ Explorer or the CLI to administer your queue manager here: https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_admin_mqcliexp
