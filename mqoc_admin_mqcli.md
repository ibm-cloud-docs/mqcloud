---
copyright:
  years: 2017, 2018
lastupdated: "2018-02-06"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administering a queue manager using runmqsc from an MQ client
{: #mqoc_admin_mqcli}

There are many actions you can perform by using runmqsc from an MQ client. You can
* Connect to a queue manager
* Create a new queue
* Put a message onto a queue
* Get a message from a queue
* Delete a queue
{:shortdesc}

---

## Prerequisites
{: #prereq_mqoc_admin_mqcli}

* An existing queue manager (for instructions, follow the [creating a queue manager](mqoc_create_qm.html) guide).
* You have been granted permissions to access queue managers within your IBM MQ service instance. You have obtained your MQ username and have created your platform API key (for instructions, follow the [configuring administrator access for a queue manager](tutorials/tut_mqoc_configure_admin_qm_access.html) guide).
* An existing installation of IBM MQ Client (download and installation instructions can be obtained from [here](http://www-01.ibm.com/support/docview.wss?uid=swg24042176)).

---

## Gather required queue manager details
{: #getdetails_mqoc_admin_mqexp}

1. Log in to the IBM Cloud console.
2. Click on the 'hamburger menu'.
3. Click **Dashboard**.
4. Locate and click on your IBM MQ service instance, found under the 'Services' heading.
  * Ensure that **RESOURCE GROUP** is set to **All Resources** and **REGION** is set to **US South Region**.
5. From the list of your queue managers, click on the one you want to administer.
6. Make note of the **Queue manager name**, **Hostname** and **Port** values for use in the next steps.

---

## Connect to your queue manager using runmqsc
{: #connect_mqoc_admin_mqcli}

1. Open a shell or PowerShell prompt to use in the next steps.
2. Export the 'MQSERVER' variable:
 * Linux: `export MQSERVER="CLOUD.ADMIN.SVRCONN/TCP/<Hostname>(<Port>)"`
 * Windows (PowerShell): `$env:MQSERVER="CLOUD.ADMIN.SVRCONN/TCP/<Hostname>(<Port>)"`
3. Export the 'MQSAMP_USER_ID' variable:
 * Linux: `export MQSAMP_USER_ID="<your MQ username>"`
 * Windows (PowerShell): `$env:MQSAMP_USER_ID="<your MQ username>"`
4. Run `$PATH_TO_MQ_BIN_DIR/runmqsc -c -u <your MQ username> -w60 <QUEUE_MANAGER_NAME>`
5. Enter your **platform API key** when prompted for a password.

---

## Create a new test queue called 'DEV.TEST.1'
{: #createq_mqoc_admin_mqcli}

**NOTE:** For the beta release of the MQ on IBM Cloud service,  queue names should start with **DEV.*** (example: DEV.myQueue) as application users have been configured with access to this prefix only.

In the same shell used in the previous steps:

1. Run `DEFINE QLOCAL (DEV.TEST.1)`
2. Run `DISPLAY QLOCAL(DEV.TEST.1)`
 * Details of queue 'DEV.TEST.1' are displayed.
3. Run `end`
 * The runmqsc session is closed.
 * Retain the prompt to use in the next steps.

---

## Put a message using the amqsputc sample program
{: #put_mqoc_admin_mqcli}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsputc 'DEV.TEST.1' <QUEUE_MANAGER_NAME>`
2. Enter your **platform API key** when prompted for a password.
3. Type in a test message.
4. Hit `Enter` twice to exit the amqsputc sample.

---

## Get a message using the amqsgetc sample program
{: #get_mqoc_admin_mqcli}

1. Call `$PATH_TO_MQ_BIN_DIR/amqsgetc 'DEV.TEST.1' <QUEUE_MANAGER_NAME>`.
2. Enter your **platform API key** when prompted for a password.

Your test message is displayed.

After a short period, the amqsputc sample program should end after finding no more messages.

---

## Delete the test queue
{: #deleteq_mqoc_admin_mqcli}

1. Run `$PATH_TO_MQ_BIN_DIR/runmqsc -c -u <your MQ username> -w60 <QUEUE_MANAGER_NAME>`
2. Enter your **platform API key** when prompted for a password.
3. Run `DELETE QLOCAL(DEV.TEST.1)`
 * You receive a message stating that the queue has been deleted.
4. Run `DISPLAY QLOCAL(DEV.TEST.1)` to prove the queue has been deleted.
 * You receive a message stating that the queue was not found.
5. Run `end`
 * The runmqsc session is closed.

---

## Conclusion
{: #conc_mqoc_admin_mqcli}

You've successfully:
* Connected to a queue manager using runmqsc and have created a new test queue
* Used amqsputc to put a test message onto the test queue and have then used amqsgetc to get the test message
* Deleted the test queue to clean up

---

## Next step
{: #next_mqoc_admin_mqcli}

[Connecting an application to a queue manager](/docs/services/mqcloud/mqoc_connect_app_qm.html)
