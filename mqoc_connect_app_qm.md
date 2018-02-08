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

# Connecting a sample application to a queue manager
{: #mqoc_connect_app_qm}
You can easily and simply connect a sample application to a queue manager.
{:shortdesc}

By completing the following task, you can:
1. Connect to an existing queue manager.
2. Put a test message onto the queue.
3. Get the test message from the queue.

---

## Prerequisites
{: #prereq_mqoc_connect_app_qm}

* An existing queue manager (for instructions, follow the [creating a queue manager](/docs/services/mqcloud/mqoc_create_qm.html) guide).
* An application has been granted permissions to access queue managers within your IBM MQ service instance. You have obtained the MQ username and API key for this application (for instructions, follow the [configuring access for connecting an application to a queue manager](/docs/services/mqcloud/mqoc_configure_app_qm_access.html) guide).
* An existing installation of IBM MQ Client (download and installation instructions can be obtained from [here](http://www-01.ibm.com/support/docview.wss?uid=swg24042176)).

---

## Prepare for connection
{: #prepconn1_mqoc_connect_app_qm}

1. Log in to the IBM Cloud console.
2. Click on the 'hamburger menu'.
3. Click **Dashboard**.
4. Locate and click on your IBM MQ service instance, found under the 'Services' heading.
  * Ensure that **RESOURCE GROUP** is set to **All Resources** and **REGION** is set to **US South Region**.
5. From the list of your queue managers, click on the one you want to connect to.
 * Make a note of the hostname and port number.
6. Open a shell or PowerShell prompt.
7. Export the 'MQSERVER' variable:
  * Linux: `export MQSERVER="CLOUD.APP.SVRCONN/TCP/<Hostname>(<Port>)"`
  * Windows (PowerShell): `$env:MQSERVER="CLOUD.APP.SVRCONN/TCP/<Hostname>(<Port>)"`
8. Export the 'MQSAMP_USER_ID' variable:
 * Linux: `export MQSAMP_USER_ID="<application MQ username>"`
 * Windows (PowerShell): `$env:MQSAMP_USER_ID="<application MQ username>"`

---

## Put a message onto the test queue using amqsputc
{: #put1_mqoc_connect_app_qm}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsputc 'DEV.QUEUE.1' <QUEUE_MANAGER_NAME>`
2. Enter the **application API key** when prompted for a password.
3. Type in a test message.
4. Press `Enter` twice to exit the amqsputc sample.

---

## Get a message using amqsgetc
{: #get1_mqoc_connect_app_qm}

1. Call `$PATH_TO_MQ_BIN_DIR/amqsgetc 'DEV.QUEUE.1' <QUEUE_MANAGER_NAME>`.
2. Enter the **application API key** when prompted for a password.

Your test message is displayed.

After a short period, the amqsgetc sample program should end after finding no more messages.

---

## Conclusion
{: #conc_mqoc_connect_app_qm}

You have successfully:
* Connected to a queue manager using a sample application
* Put a test message onto a queue
* Obtained the test message from the queue
