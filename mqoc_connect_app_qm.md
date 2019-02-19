---
copyright:
  years: 2017, 2019
lastupdated: "2018-03-05"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting a sample application to a queue manager
{: #mqoc_connect_app_qm}
You can easily and simply connect an application to a queue manager. You can run your application in a number of ways, deployed in the cloud for instance. For validation purposes and the purposes of this example, you can run the IBM MQ sample applications from your own machine (your laptop for example).
{:shortdesc}

By completing the following task, you can:
1. Connect to an existing queue manager using the IBM MQ Client samples from your own machine.
2. Put a test message onto a queue.
3. Get the test message from a queue.

---

## Prerequisites
{: #prereq_mqoc_connect_app_qm}

* An existing queue manager (for instructions, follow the [creating a queue manager](/docs/services/mqcloud/mqoc_create_qm.html) guide).
* An application has been granted permissions to access queue managers within your IBM MQ service instance. You have obtained the MQ username and API key for this application (for instructions, follow the [configuring access for connecting an application to a queue manager](/docs/services/mqcloud/mqoc_configure_app_qm_access.html) guide).
* An existing installation of IBM MQ Client on your own machine.
 * Download the client from [here](http://www-01.ibm.com/support/docview.wss?uid=swg24042176#1).
   * Clicking the **HTTP** link next to the latest available version of the **CD Clients** will take you to **Fix Central**. From there you can search for and select the appropriate **Redist** (redistributable) client bundle for your operating system platform. This will include the sample applications.
   * Once downloaded, unpack the bundle into a location of your choosing.
   * Make a note of the full path to the directory containing the sample applications. This path will be referenced as `<PATH_TO_SAMPLE_BIN_DIR>` for the rest of this task.
     * For Windows, this will be the `bin` directory unpacked in the previous step, the location of which will depend upon where you chose to unpack the bundle.
     * For Linux, this will be the `samp/bin` directory unpacked in the previous step, the location of which will depend upon where you chose to unpack the bundle.

---

## Prepare for connection
{: #prepconn1_mqoc_connect_app_qm}

Open a web browser and log in to the IBM Cloud console.

1. Click on the 'hamburger menu'.
2. Click **Dashboard**.
 * Ensure that **RESOURCE GROUP** is set to **All Resources**.
3. Locate and click on your IBM MQ service instance, found under the 'Services' heading.
4. From the list of your queue managers, click on the one you want to connect to.
 * Make a note of the hostname and port number.

Open a command shell on your own machine.
1. Set the 'MQSERVER' variable:
 * Linux: `export MQSERVER="CLOUD.APP.SVRCONN/TCP/<Hostname>(<Port>)"`
 * Windows (Command prompt): `set MQSERVER=CLOUD.APP.SVRCONN/TCP/<Hostname>(<Port>)`
 * Windows (PowerShell): `$env:MQSERVER="CLOUD.APP.SVRCONN/TCP/<Hostname>(<Port>)"`

2. Set the 'MQSAMP_USER_ID' variable:
 * Linux: `export MQSAMP_USER_ID="<application MQ username>"`
 * Windows (Command prompt): `set MQSAMP_USER_ID=<application MQ username>`
 * Windows (PowerShell): `$env:MQSAMP_USER_ID="<application MQ username

  **Note:** The next steps should be run from this same command shell.

---

## Put a message onto the test queue using amqsputc
{: #put1_mqoc_connect_app_qm}

**Note: ** Please ensure that you have carried out the prerequisite steps listed above - in particular configuring application access to the queue manager.

In the same shell used in the previous step:

1. Run `<PATH_TO_SAMPLE_BIN_DIR>/amqsputc DEV.QUEUE.1`
 * Where `<PATH_TO_SAMPLE_BIN_DIR>` is the path to the sample applications bin directory you made note of in the Prerequisites section above.
2. Enter the **application API key** when prompted for a password.
3. Type in a test message.
4. Press `Enter` twice to exit the amqsputc sample.

---

## Get a message using amqsgetc
{: #get1_mqoc_connect_app_qm}

In the same shell used in the previous step:

1. Run `<PATH_TO_SAMPLE_BIN_DIR>/amqsgetc DEV.QUEUE.1`
 * Where `<PATH_TO_SAMPLE_BIN_DIR>` is the path to the sample applications bin directory you made note of in the Prerequisites section above.
2. Enter the **application API key** when prompted for a password.

Your test message is displayed.

After a short period, the amqsgetc sample program should end after finding no more messages.

---

## Conclusion
{: #conc_mqoc_connect_app_qm}

You have successfully:
* Connected to a queue manager using a sample application from your own machine.
* Put a test message onto a queue.
* Obtained the test message from the queue.
