---
copyright:
  years: 2017, 2026
lastupdated: "2026-01-22"

subcollection: mqcloud

keywords: started, guided, tour
---

{{site.data.keyword.attribute-definition-list}}

# Getting started
{: #getting_started}

{{site.data.keyword.mq_full}} enables you to quickly and easily deploy queue managers in the cloud and connect your applications to them, for reliable data transfer between different parts of your enterprise application landscape.
{: shortdesc}

This document describes two approaches to get started with {{site.data.keyword.mq_full}}:

- **Getting started using the Guided Tour** - this describes how to start the embedded tutorial, which will guide you through the process of creating and using your first {{site.data.keyword.mq_full}} queue manager.
- **Manually creating and using an {{site.data.keyword.mq_full}} queue manager** - this provides documented steps describing how to create and use your first {{site.data.keyword.mq_full}} queue manager.

## Before you begin
{: #getting_started_prepreqs}

* You need an [{{site.data.keyword.cloud}}](https://cloud.ibm.com/registration/) account.
* Permissions to create an {{site.data.keyword.mq_full}} instance in the account.

## Creating an {{site.data.keyword.mq_full}} instance
{: #getting_started_create_instance}

To create an {{site.data.keyword.mq_full}} instance:

1. Go to the [{{site.data.keyword.cloud_notm}} **Catalog**](https://cloud.ibm.com/catalog?category=integration){: external}
2. Select **MQ**
3. Select your desired region.
4. Type in a service name.
5. Select a plan, for example **Lite**.
6. Click **Create**.

You are now presented with a view of your service instance from where you can view and manage your queue managers. This is also the page from which you can launch the Guided Tour.

## Getting started using the Guided Tour
{: #getting_started_guided_tour}

{{site.data.keyword.mq_full}} comes with a Guided Tour, which provides step by step guidance through the following steps:

- Creating a queue manager
- Registering an application to put and get messages on a queue
- Administering a queue manager

You can launch the Guided Tour by selecting the Guided tours item from the help menu on the IBM Cloud header bar. Click 'Get started', then select one of the available tours.

## Manually creating and using an {{site.data.keyword.mq_full}} queue manager
{: #getting_started_manual_create}

As an alternative to the Guided Tour, you can instead follow the documented steps below to create and use the {{site.data.keyword.mq_full}} service:

1. [Creating a queue manager](https://www.ibm.com/docs/SSCL78/mqoc_create_qm.html){: external}
2. [Administering a queue manager using the IBM MQ Console](https://www.ibm.com/docs/SSCL78/admin_console.html){: external}
3. [Connecting a sample application to a queue manager](https://www.ibm.com/docs/SSCL78/connectsample.html){: external}
