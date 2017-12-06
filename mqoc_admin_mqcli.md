---
copyright:
  years: 2017
lastupdated: "2017-12-6"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administering a queue manager using runmqsc from an MQ client
{: #mqoc_admin_mqcli}

You can manage a queue using runmqsc from an MQ client. You can connect to a queue manager, create a new queue, put a message onto the queue, get a message from the queue, and delete the queue.
{:shortdesc}

---

## Prerequisites
{: #prereq_mqoc_admin_mqcli}

* An existing queue manager (for instructions, follow the [creating a queue manager](mqoc_create_qm.html) guide).
* An administrative user and API key (for instructions, follow the [configuring administrator access for a queue manager](tutorials/tut_mqoc_configure_admin_qm_access.html) guide).
* An existing installation of IBM MQ Client (download and installation instructions can be obtained from [here](http://www-01.ibm.com/support/docview.wss?uid=swg24042176)).

---

## Gather required queue manager details
{: #getdetails_mqoc_admin_mqexp}

1. Log in to the IBM Cloud console.
2. Click on the 'hamburger menu'.
3. Click **Dashboard**.
4. Locate and click on your IBM MQ service instance, found under the 'Cloud foundry Services' heading.
5. From the list of your queue managers, click on the one you want to administer.
6. Make note of the **Queue manager name**, **Hostname** and **Port** values for use in the next steps.

---

## Connect to your queue manager using runmqsc
{: #connect_mqoc_admin_mqcli}

1. Open a shell or PowerShell prompt to use in the next steps.
2. Export the 'MQSERVER' variable:
 * Linux: `export MQSERVER="CLOUD.ADMIN.SVRCONN/TCP/$Hostname($Port)"`
 * Windows (PowerShell): `$env:MQSERVER="CLOUD.ADMIN.SVRCONN/TCP/$Hostname($Port)"`
3. Export the 'MQSAMP_USER_ID' variable:
 * Linux: `export MQSAMP_USER_ID="admin"`
 * Windows (PowerShell): `$env:MQSAMP_USER_ID="admin"`
4. Run `$PATH_TO_MQ_BIN_DIR/runmqsc -c -u admin -w60 $QUEUE_MANAGER_NAME`
5. Enter your admin user API key when prompted.

---

## Create a new test queue called 'CLOUD.TEST.1'
{: #createq_mqoc_admin_mqcli}

**NOTE:** For the experimental release of the MQ on IBM Cloud service,  queue names should start with **CLOUD.*** (example: CLOUD.myQueue) as application users have been configured with access to this prefix only.

In the same shell used in the previous steps:

1. Run `DEFINE QLOCAL (CLOUD.TEST.1)`
2. Run `DISPLAY QLOCAL(CLOUD.TEST.1)`
 * Details of queue 'CLOUD.TEST.1' are displayed.
3. Run `end`
 * The runmqsc session is closed.
 * Retain the prompt to use in the next steps.

---

## Put a message using the amqsputc sample program
{: #put_mqoc_admin_mqcli}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsputc 'CLOUD.TEST.1' $QUEUE_MANAGER_NAME`
2. Enter your admin user API key when prompted for a password.
3. Type in a test message.
4. Hit `Enter` twice to exit the amqsputc sample.

---

## Get a message using the amqsgetc sample program
{: #get_mqoc_admin_mqcli}

1. Call `$PATH_TO_MQ_BIN_DIR/amqsgetc 'CLOUD.TEST.1' $QUEUE_MANAGER_NAME`.
2. Enter your admin user API key when prompted for a password.

Your test message is displayed.

After a short period, the amqsputc sample program should end after finding no more messages.

---

## Delete the test queue
{: #deleteq_mqoc_admin_mqcli}

1. Run `$PATH_TO_MQ_BIN_DIR/runmqsc -c -u admin -w60 $QUEUE_MANAGER_NAME`
2. Enter your admin user API key when prompted.
3. Run `DELETE QLOCAL(CLOUD.TEST.1)`
 * You receive a message stating that the queue has been deleted.
4. Run `DISPLAY QLOCAL(CLOUD.TEST.1)` to prove the queue has been deleted.
 * You receive a message stating that the queue was not found.
5. Run `end`
 * The runmqsc session is closed.

---

## Conclusion
{: #conc_mqoc_admin_mqcli}

You've successfully connected to a queue manager using runmqsc and have created a new test queue. You have used amqsputc to put a test message onto the test queue and have then used amqsgetc to get the test message. You have then deleted the test queue to clean up.

---

## Next step
{: #next_mqoc_admin_mqcli}

[Connecting an application to a queue manager](/docs/services/mqcloud/mqoc_connect_app_qm.html)
