---
copyright:
  years: 2020, 2021
lastupdated: "2021-09-27"

subcollection: mqcloud

keywords: connect, access, client, queue, manager, permissions
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Assigning user/group access to a queue
{: #mqoc_configure_auth_record}

The default configuration of an {{site.data.keyword.mq_full}} queue manager is for all initial queues to be assigned with authority records, allowing users and applications to send and receive messages. All queues and topics beginning with 'DEV.' are configured to allow messages to be sent and received.

If a new queue or topic has been created whose name does not start with 'DEV.' the predefined authorization records will not apply. Therefore applications will not have the required permissions to send or receive messages to this queue or topic.

In this case attempting to send a message to a new queue whose name does not begin with 'DEV', will result in one of the below error messages:

* `JMSWMQ2007: Failed to send a message to destination '[YOUR QUEUE NAME]'`
* `MQRC_NOT_AUTHORIZED (2035)`.

##  Configuring authority records

Using one of the following methods.

* Using `runmqsc`, run the following commands:

  `SET AUTHREC PROFILE('TEST.QUEUE') OBJTYPE(QUEUE) GROUP('demoapp') AUTHADD(PUT,GET,BROWSE,INQ)`

  `SET AUTHREC PROFILE('TEST.QUEUE') OBJTYPE(TOPIC) GROUP('demoapp') AUTHADD(SUB,PUB)`

  *Note:* replace 'TEST.QUEUE' with the name of your queue., and 'demoapp' wither your application username.  If you wish, you can grant access to an object to all connected applications by specifying the group 'mqwriter'.

* Via the web console:

  - Select the new queue then 'Configuration' under the three dots at the top of the screen.
  - Select 'Security' and click 'Add +'.
  - Select 'Group' and enter the name 'mqwriter' as the 'Group Name'. Tick the 'MQI' checkbox, and ensure only the boxes below MQI are checked.
  - Click the  'Create' button.