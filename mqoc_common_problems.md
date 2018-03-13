---
copyright:
  years: 2018
lastupdated: "2018-02-22"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Common problems faced using the MQ on IBM Cloud service
{: #mqoc_problem_intro}

This document contains information about common questions or problems encountered by users of the MQ on IBM Cloud service. It aims to answer questions or provide instruction on how to resolve issues without the need to raise a support ticket.
{:shortdesc}

When attempting to diagnose a problem with your queue manager the first place you should look is your queue manager logs. You can find information on how to download your queue manager logs on the [Downloading queue manager logs and diagnostics page](/docs/services/mqcloud/mqoc_download_logs.html)

---

## Client application or client queue manager cannot connect with reason code MQRC_MAX_CONNS_LIMIT_REACHED (2025)
{: #mqoc_client_conn_limit}

While attempting to connect a client application or queue manager to your MQ on IBM Cloud queue manager you receive a return code of `MQRC_MAX_CONNS_LIMIT_REACHED` (2025) and the client cannot connect.

Additionally, an error message is outputted with title `AMQ9694E: Program cannot connect because connection limit reached.`

### Explanation
{: #mqoc_client_conn_limit_explain}

MQ on IBM Cloud applies limits to queue managers resources based on size. The values of each limit, and what are limited, are detailed in the information about each queue manager size when you create a new queue manager.

One of the limits applied to the queue manager is the number of concurrent client connections, this applies to both client applications and client queue managers. If you attempt to exceed the number of allowed connections your client application is blocked with the return code `MQRC_MAX_CONNS_LIMIT_REACHED` (2025) and an `AMQ9694E` error message is printed in the queue manager logs.

*Note:* Because JMS uses two client connections to pass messages you need to be aware that if your queue manager connection limit is 10 you can only connect 5 JMS clients to your queue manager before reaching the connection limit.

### Solution
{: #mqoc_client_conn_limit_solution}

To resolve this problem either:

* Disconnect unnecessary client connections to allow newer clients to connect
or
* Upgrade your queue manager to a larger size to allow more client connections.

To let you know when you are getting close to your queue manager client connection limit, the queue manager outputs an `AMQ7358W` error message in the queue manager logs when it is at 80% of allowed client connections.

---

## You receive a MQRCCF_ACCESS_BLOCKED (3382) return code when attempting to administer queue manager
{: #mqoc_client_conn_blocked}

While attempting to define, delete or alter objects in your MQ on IBM Cloud queue manager your administration client receives an `MQRCCF_ACCESS_BLOCKED` (3382) return code. With clients running versions of IBM MQ v9.0.3 and below you might receive a return code of `MQRC_UNEXPECTED_ERROR` (2195)

Additionally, an error message is outputted with title `AMQ7355E: Object <Object name>, object type <Object type>, is locked to remote users.`

### Explanation
{: #mqoc_client_conn_blocked_explain}

Certain features of IBM MQ have been disabled for users of MQ on IBM Cloud. These features are disabled either to prevent accidentally disabling the queue manager or potential misuse of the service. You might see that some of the locked attributes have values assigned to them, these are assigned automatically and cannot be changed.

If you try to define, alter or delete an object or attribute that has been disabled, your queue manager blocks this action with the return code `MQRCCF_ACCESS_BLOCKED` (3382). This return code was added at version 9.0.3 of IBM MQ, clients that are older than version 9.0.3 will not recognize this return code and so are likely to return `MQRC_UNEXPECTED_ERROR` (2195) instead.

The following features have been disabled:

* The following queue manager attributes: `CONNAUTH`, `CHADEXIT`, `CLWLEXIT`, `CLWLDATA`, `SSLCRYP`, `SSLKEYR`
* Authentication information objects of type `IDPWOS` & `IDPWLDAP`
* The following channel attributes: `MSGEXIT`, `MSGDATA`, `SCYEXIT`, `SCYDATA`, `SENDEXIT`, `SENDDATA`, `RCVEXIT`, `RCVDATA`
* Listener objects.
* Service objects. *Note:* You can start or stop an existing service object.
* Process objects.
* The following queue attributes: `PROCESS`, `INITQ`, `TRIGDATA`, `TRIGDPTH`, `TRIGGER`, `NOTRIGGER`, `TRIGMPRI`, `TRIGTYPE`
* `COMMINFO` objects.

---

## Client application or client queue manager cannot connect to a newly created channel
{: #mqoc_new_channel}

While attempting to connect a client application or queue manager to your MQ on IBM Cloud queue manager via a channel you have recently created you receive a return code of `MQRC_NOT_AUTHORIZED` (2035) and the client cannot connect.

Additionally, an error message is outputted with title `AMQ9777E: Channel was blocked`

### Explanation
{: #mqoc_new_channel_explain}

The default configuration of a MQ on IBM Cloud queue manager creates a channel authentication rule that blocks all connections except connections to the channels `CLOUD.ADMIN.SVRCONN` and `CLOUD.DEV.SVRCONN`. If you create a new channel, no clients will be able to connect via that channel as they will be blocked by the channel authentication rule `CHLAUTH('*') TYPE(ADDRESSMAP) ADDRESS('*') USERSRC(NOACCESS)`

### Solution
{: #mqoc_new_channel_solution}

To resolve this problem create a new channel authentication rule that allows access to your channel. For example, if you have a channel called `QM.ENTRY` then create a channel authentication rule with the following values: `CHLAUTH('QM.ENTRY') TYPE(ADDRESSMAP) ADDRESS('*') USERSRC(CHANNEL)`

---

## Java or JMS Client application receives a return code of `MQRC_NOT_AUTHORIZED` (2035) and the client cannot connect even though a userid and password is supplied.
{: #mqoc_jms_user_id}

While attempting to connect a Java or JMS client application to your MQ on IBM Cloud queue manager you receive a return code of `MQRC_NOT_AUTHORIZED` (2035) and the client cannot connect. Additionally, an error message is outputted with title `AMQ9791E: The client application did not supply a user ID and password.`.

### Explanation
{: #mqoc_jms_user_id_explain}

The default configuration of a MQ on IBM Cloud queue manager specifies that any application connecting to the queue manager must supply valid user credentials. Users and applications can have credentials created by following the instructions in the [Users and Applications document page](mqoc_configure_users_and_apps.html). When connecting an application you must ensure to supply these credentials otherwise the connecting application will be unable to connect.

Java and JMS applications have two different methods of supplying credentials to a queue manager that is controlled by a switch called `compatibility mode`. You must ensure that when the Java or JMS application is connecting it is supplying user credentials with compatibility mode disabled.

Client applications connecting using IBM MQ client libraries below version 8.0.0.0 will be unable to supply user credentials to the queue manager and so will be unable to connect.

### Solution
{: #mqoc_jms_user_id_solution}

To resolve this issue follow these steps:

1. Ensure that the IBM MQ client libraries being used are version 8.0.0.0 or above.
2. Ensure that the client application is supplying valid user credentials in the `MQCSP` structure. For more information on the `MQCSP` structure see [the following Knowledge Center page](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.ref.dev.doc/q095620_.htm)
3. If using a Java or JMS application, ensure that comptability mode is not enabled. See [this knowledge center page for more information](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_8.0.0/com.ibm.mq.sec.doc/q118680_.htm)
