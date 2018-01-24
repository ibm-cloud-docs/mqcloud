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

# Connecting a sample application to a queue manager
{: #mqoc_connect_app_qm}
You can easily and simply connect a sample application to a queue manager.
{:shortdesc}

By completing the following task, you can:
1. Connect to an existing queue manager using user **app1**.
2. Put a test message onto an existing queue using user **app1**.
3. Get the test message from the queue using user **app1**.
4. Put a second test message onto an existing queue using user **app1**.
5. Connect to the same queue manager using user **app2**.
6. Get the test message from the queue using user **app2**.
7. Clear the test queue of messages.

---

## Prerequisites
{: #prereq_mqoc_connect_app_qm}

* An existing queue manager (for instructions, follow the [creating a queue manager](/docs/services/mqcloud/mqoc_create_qm.html) guide).
* The [necessary credentials](/docs/services/mqcloud/mqoc_configure_app_qm_access.html) for both an **app1** and **app2** user to connect an application to a queue manager.
* An existing installation of IBM MQ Client (download and installation instructions can be obtained from [here](http://www-01.ibm.com/support/docview.wss?uid=swg24042176)).

---

## Prepare for connection with user app1
{: #prepconn1_mqoc_connect_app_qm}

1. Log in to the IBM Cloud console.
2. Click on the 'hamburger menu'.
3. Click **Dashboard**.
4. Locate and click on your IBM MQ service instance, found under the 'Cloud foundry Services' heading.
5. From the list of your queue managers, click on the one you want to connect to.
 * Make a note of the hostname and port number.
6. Open a shell or PowerShell prompt.
7. Export the 'MQSERVER' variable:
  * Linux: `export MQSERVER="CLOUD.APP.SVRCONN/TCP/$Hostname($Port)"`
  * Windows (PowerShell): `$env:MQSERVER="CLOUD.APP.SVRCONN/TCP/$Hostname($Port)"`
8. Export the 'MQSAMP_USER_ID' variable:
 * Linux: `export MQSAMP_USER_ID="app1"`
 * Windows (PowerShell): `$env:MQSAMP_USER_ID="app1"`

---

## Put a message onto the test queue with user app1 using amqsputc
{: #put1_mqoc_connect_app_qm}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsputc 'DEV.QUEUE.1' $QUEUE_MANAGER_NAME`
2. Enter your **app1** user API key when prompted for a password.
3. Type in a test message.
4. Press `Enter` twice to exit the amqsputc sample.

---

## Get a message with user app1 using amqsgetc
{: #get1_mqoc_connect_app_qm}

1. Call `$PATH_TO_MQ_BIN_DIR/amqsgetc 'DEV.QUEUE.1' $QUEUE_MANAGER_NAME`.
2. Enter your **app1** user API key when prompted for a password.

Your test message is displayed.

After a short period, the amqsgetc sample program should end after finding no more messages.

---

## Put a second message onto the test queue with user app1 using amqsputc
{: #put2_mqoc_connect_app_qm}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsputc 'DEV.QUEUE.1' $QUEUE_MANAGER_NAME`
2. Enter your **app1** user API key when prompted for a password.
3. Type in a test message.
4. Press `Enter` twice to exit the amqsputc sample.

---

## Prepare for connection with user app2
{: #prepconn2_mqoc_connect_app_qm}

1. Open a new shell or PowerShell prompt.
2. Export the 'MQSERVER' variable:
 * Linux: `export MQSERVER="CLOUD.APP.SVRCONN/TCP/$Hostname($Port)"`
 * Windows (PowerShell): `$env:MQSERVER="CLOUD.APP.SVRCONN/TCP/$Hostname($Port)"`
3. Export the 'MQSAMP_USER_ID' variable:
 * Linux: `export MQSAMP_USER_ID="app2"`
 * Windows (PowerShell): `$env:MQSAMP_USER_ID="app2"`

---

## Get a message with user app2 using amqsgetc
{: #get2_mqoc_connect_app_qm}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsgetc 'DEV.QUEUE.1' $QUEUE_MANAGER_NAME`
2. Enter your **app2** user API key when prompted for a password.

Your test message is displayed.

After a short period, the amqsgetc sample program should end after finding no more messages.

---

## Attempt to put a message with user app2 using amqsputc
{: #put3_mqoc_connect_app_qm}

1. Run `$PATH_TO_MQ_BIN_DIR/amqsputc 'DEV.QUEUE.1' $QUEUE_MANAGER_NAME`
2. Enter your **app2** user API key when prompted for a password.

The amqsputc sample program ends with a return message of: **with reason code 2035**.

---

## Conclusion
{: #conc_mqoc_connect_app_qm}

You have successfully:
* Connected to a queue manager using a sample application with an application id
* Put a test message onto a queue using an application id with read/write authority
* Gotten the test message using ids with read/write and read only authority
* Proved that the id with read only authority was not able to put a message
