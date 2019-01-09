---
copyright:
  years: 2017, 2018
lastupdated: "2018-01-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# New To IBM MQ
{: #index}

<p align="center">
<img src="./images/IBM-MQ-Sticker.png?raw=true" alt="Image of MQ Logo"/>
</p>

IBM MQ is an enterprise grade messaging middleware service that gives independent and potentially non-concurrent applications secure messaging capabilities, such as point-to-point and publish/subscribe models. MQ has been proving itself as an effective messaging solution for more than 25 years. The recently released MQ on Cloud enables you to use IBM MQ as a managed offering, therefore IBM will handle upgrades, patches and also many of the operational management tasks, allowing you to focus on the integration of MQ with your applications.
In addition to the cloud service, IBM MQ is available in a wide range of customer-managed deployment form factors such as software for many operating systems including Linux and Windows. It is available as a containerised application and within a Kubernetes cluster, it is even available as something known as the MQ appliance which is dedicated hardware for running MQ. It is also available on the IBM z/OS mainframe.

## Why would I use MQ

When someone builds a network to process thousands of transactions every minute, one needs to ensure that not even a single transaction is lost. If the servers are unable to process the number of transactions fast enough it is highly likely that transactions may be lost. MQ works by storing the transactions to be processed on a message queue and then processing them one at a time. This allows transactions to be processed at a flat rate meaning that extra CPU during high demand times is not required. It also means that if the system were to suddenly break down, the messages that are being processed are safely stored on the message queue and will not be lost.

IBM MQ integrates with many different operating systems and languages, from older languages such as COBOL to newer ones such as Node.js. You can seamlessly integrate applications across a verity of platforms and use a wide range of APIs. MQ carries out all necessary data transformations for you. Once MQ is integrated on your system you no longer need to worry about the complexities of securely transforming and sending a message as MQ carries out all of this for you including encryption and decryption.

Learn how IBM MQ is different to other messaging solutions and other frequently asked questions here: https://www.IBM.com/products/mq/faq

## Learn MQ

IBM MQ is the most powerful messaging solution available on the market, it enables applications to communicate and share data with one another, it is highly scaleable and can be applied to a wide range of business needs, learn how IBM MQ can benefit your application scenario here: https://developer.IBM.com/messaging/learn-mq/mq-tutorials/getting-started-mq/

You can try MQ for free and without the need for any expensive infrastructure costs by creating a trial in IBM Cloud. MQ on Cloud has been developed with ease of use in mind and requires no specialist knowledge to use. You can find instructions on how to deploy a queue manager in IBM Cloud here: https://developer.IBM.com/messaging/learn-mq/mq-tutorials/mq-connect-to-queue-manager/#cloud

Interested in proving your knowledge? Become an MQ expert and prove your knowledge with the official IBM MQ developer badge, you will be able to work your way through some tutorials and learn all MQ fundamentals as well as some more in depth knowledge of creating applications that can utilise MQ to communicate: https://developer.IBM.com/messaging/learn-mq/mq-tutorials/mq-dev-essentials/

## Administrating an MQ on Cloud queue manager

MQ on Cloud still allows you to use all of the traditional MQ administration tools, including a web based version of the MQ console. You can find instructions on how to use the console here: https://console.bluemix.net/docs/services/mqcloud/mqoc_admin_mqweb.html#mqoc_admin_mqweb

MQ on Cloud can be administered via locally installed tools too. MQ explorer is a locally installed Eclipse-based tool for administering IBM MQ which you can install on a machine of your choosing, it connects to MQ on Cloud using a client connection and is supported on both Windows and Linux based environments, however, it is unavailable on Mac OS. You can learn more about using MQ explorer here: https://console.bluemix.net/docs/services/mqcloud/mqoc_admin_mqexp.html#mqoc_admin_mqexp.

There is also a Command Line Interface available which can be used to administer MQ on Cloud. The CLI enables the ability to create scripts containing groups of MQ commands so that many different tasks can be carried out at the same time. It can be installed as part of the MQ clients bundle and is available on Linux and windows, however is unavailable on Mac OS. You can learn more about using the CLI to administer your queue manager here: https://console.bluemix.net/docs/services/mqcloud/mqoc_admin_mqcli.html#mqoc_admin_mqcli

---
# Getting started with MQ on IBM Cloud
{: #index}

MQ on IBM Cloud enables you to quickly and easily deploy queue managers in the cloud and connect your applications to them, for reliable data transfer between different parts of your enterprise application landscape.

This document describes two approaches to get started with IBM MQ on Cloud:
  - **Getting started using the Guided Tour** - this describes how to start the embedded tutorial, which will guide you through the process of creating and using your first IBM MQ on Cloud queue manager.
  - **Manually creating and using an IBM MQ on Cloud queue manager** - this provides documented steps describing how to create and use your first IBM MQ on Cloud queue manager.

---

## Getting started using the Guided Tour
{: #index_guidedtour}

The MQ on Cloud service comes with a Guided Tour, which provides step by step guidance through the following steps:
 - creating a queue manager
 - creating an administrator user
 - using a demo application to put and get messages on a queue
 - accessing the IBM MQ Web Console

Before you can create the queue manager, you need to create a service instance, which is described in the next section 'Launching MQ on IBM Cloud'

### Launching MQ on IBM Cloud
{: #launch_mqoc_create_qm}

In order to access the Guided Tour, you must first launch the IBM MQ on Cloud service, which is achieved by creating an IBM MQ on Cloud service instance.

To create an MQ on Cloud service instance:
1. Log in to the IBM Cloud console, accessible at: http://console.bluemix.net/
2. Click **Catalog**.
3. Click **Integration**, and
4. Click **MQ**.
5. Type in a service name.
6. Select a plan, for example **Default**.
7. Click **Create**.

You are now presented with a view of your service instance from where you will be able to view and manage your queue managers. This is also the page from which you can launch the Guided Tour.

### Using the Guided Tour

You can launch the Guided Tour by clicking on the folding icon at the top right of the page.

![Image showing the location of the Guided Tour start icon](./images/mqoc_getting_started_gt_icon.png)

**Note:** if you don't yet have any queue managers, the Guided Tour will automatically be expanded.

Once the Guided Tour is expanded, you can begin by clicking 'Get Started'.

![Image showing the location of the Guided Tour start icon](./images/mqoc_getting_started_gt_open.png)

---

## Manually creating and using an IBM MQ on Cloud queue manager
{: #index_manual}

As an alternative to the Guided Tour, you can instead follow the documented steps below to create and use the IBM MQ on Cloud service:

1. [Create a queue manager.](/docs/services/mqcloud/mqoc_create_qm.html)
2. [Administer a queue manager](/docs/services/mqcloud/mqoc_admin_mqweb.html) using the IBM MQ Web Console.
3. [Connect a sample application to a queue manager.](/docs/services/mqcloud/mqoc_connect_app_qm.html)
