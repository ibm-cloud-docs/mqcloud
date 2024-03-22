---
copyright:
  years: 2017, 2021
lastupdated: "2021-09-29"

subcollection: mqcloud

keywords: connect, onprem, direct
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Direct connection to an on-premises queue manager
{: #mqoc_connect_onprem_direct}

The following guide explains how to connect an IBM MQ on Cloud queue manager to an on-premises queue manager, configure TLS security, and send messages between the two queue managers. This is applicable to users who have deployed a queue manager using the Lite, Default, or Custom plans. It's worth noting that the instructions outlined here are not suitable for queue managers deployed under the reserved deployment plan. This is because of the intricate private networking configurations associated with such deployments.
{: shortdesc}  

The following steps help you configure the connection between the two queue managers, making this connection secure, and capable of sending messages bidirectionally.

* Create the queues in the MQ On Cloud queue manager.

    * A remote queue to hold messages from the cloud application that is connected to a transmit queue.
    * A local queue to hold responses from the on-premises queue manager requester channel.


* Create the channels and authorizations to allow the MQ On Cloud queue manager to connect.

    * The server channel - this channel receives the initial connection from the on-premises queue manager, and forwards the messages from the transmit queue.
    * A receiver channel - this channel receives responses from the on-premises sender channel.


* Create the queues in the on-premises queue manager.

    * A local queue - this queue holds messages that are destined for the on-premises application
    * A remote queue - this queue is connected to a transmit queue to hold responses from the on-premises application
    destined for the cloud queue manager.


* Create the channels and authorization to connect to the MQ On Cloud queue manager.

    * A requester channel - this channel corresponds to the server channel on the cloud - connected to the local queue.
    * A sender channel - this channel corresponds to the receiver channel on the cloud queue manager - accepting
    messages from the transmit queue and forwarding them to the cloud queue manager.


* Set up TLS security by giving the local queue manager the certificates to permit a trust relationship between the two queue managers.


![alt text][connect_on_prem1] 

[connect_on_prem1]: ./images/mqoc_connect_onprem1.png "Direct Connection"

The following documented steps involve detailed explanation on how to securely transfer messages between an application that is deployed in IBM Cloud and an application running in an on-premises data center, using IBM MQ to provide the reliable secure connection between the two deployments.

## Before you begin

1. There are two components in this system, which you need to have setup and installed.

    * A cloud-hosted queue manager deployed using the MQ service in IBM Cloud. In the following steps this is referred to as "MyCloudQM".
        - For instructions to create queue manager, follow the [creating a queue manager](/docs/services/mqcloud?topic=mqcloud-mqoc_create_qm) guide.

    * An on-premises queue manager that will be connected to the cloud queue manager. In the following steps this is referred to as "ONPREM_QM".
        - You can run an IBM MQ queue manager container locally to test this out if you do not already have a queue manager deployed. For instructions to create one, follow the [get an IBM MQ queue for development in a container](https://developer.ibm.com/tutorials/mq-connect-app-queue-manager-containers/){: external} tutorial.

    * For guidance on queue manager administration procedures, please refer to the [Queue manager administration options](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_admin_qm)        
    

2. Obtain connection details of the cloud queue manager for later use as follows:

    * Log in to your service instance in the IBM Cloud service console

    * Click on the row in the list that represents your queue manager in order to view its details

    * Click the "Connection Information" button and select "JSON CCDT" from the resulting dialog box

    * Save the json file for later use

        In particular it is important that you make note of the queue manager name, the hostname, and the listener port from the downloaded connection details as you will use them in the following sections.

3. Obtain the public queue manager cert of the cloud queue manager for later use as follows:

    * Log in to your service instance in the IBM Cloud service console

    * Click on the row in the list that represents your queue manager to view its details

    * Click on the *Key store* tab, and spot the default qmgrcert. Click on the hamburger symbol and click on *Download public certificate*

##  Configuring the queue managers

### On-premises queue manager

It is important to note that the scenario that is given in the following guide assumes that the on-premises queue manager cannot be contacted directly by the Cloud queue manager (MyCloudQM) because it has no publicly reachable IP address. You must replace the traditional Sender-Receiver channels with Requester-Server channels.

* Open two command prompts, one for the on-premises queue manager and another for the cloud queue manager

* Connect to on-prem queue manager. Run *runmqsc* to connect to your remote queue manager and confirm you are successfully connected by pinging the queue manager

    ```bash
    runmqsc 
    PING QMGR
    ```

* Create the queues in the on-premises queue manager.

    ```bash
    DEFINE QLOCAL(LOCAL) 
    DEFINE QLOCAL(TO.CLOUD) USAGE(XMITQ)
    DEFINE QREMOTE(LOCAL.REPLY) RNAME(LOCAL.REPLY) RQMNAME('MyCloudQM') XMITQ(TO.CLOUD)
    ```
    -  local queue that the on-premises application would consume from
    -  transmit queue that will be used for the on-prem sender channel
    -  remote queue definition to route reply messages back to the cloud queue manager

* Create the channels and authorizations to allow the MQ On Cloud queue manager to connect.

  - on-premises sender channel that will connect to the cloud

    ```bash
    DEFINE CHANNEL(ONPREM.TO.CLOUD) CHLTYPE(SDR) +
    CONNAME('<HOSTNAME>(<PORT>)') XMITQ(TO.CLOUD) TRPTYPE(TCP)
    ```
    - `<HOSTNAME>` - this is 'host' in the file connection_info.ccdt.json
     - `<PORT>` - this is 'port' in the file connection_info.ccdt.json

   - requester channel that will call out from on-prem queue manager

     ```bash
     DEFINE CHANNEL(CLOUD.TO.ONPREM) CHLTYPE(RQSTR) +
     CONNAME('<HOSTNAME>(<PORT>)') TRPTYPE(TCP)
     ```

* Create the authentication record to allow incoming connections from the cloud QM

    ```bash
    SET CHLAUTH(CLOUD.TO.ONPREM) TYPE(QMGRMAP) QMNAME('MyCloudQM') ACTION(ADD) USERSRC(CHANNEL)
    ```
* Create and configure the key repository by following the steps below for the onprem queuemanager. 

* Change directory into the ‘ssl’ directory for your queue manager. For example, on a Windows machine this would generally be in `c:\ProgramData\IBM\MQ\qmgrs\<qmname>\ssl`. On a Linux system, it would usually be found
in `/var/mqm/qmgrs/<qmname>/ssl`.If you already have a ‘key.kdb’ file ( key/trust store ) in this directory, you can can skip the next step. Otherwise, you will now use the “runmqakm” command to create a key store:


   ```bash

   runmqakm -keydb -create -db key.kdb -pw passOwrd -type pkcs12 -expire 0 -stash
   chmod +rw key.kdb

   ```
* Create a self signed certificate with label `ibmmqonpremqm`

    ```bash

        runmqakm -cert -create -db key.kdb -stashed -dn "CN=LOCALQM O=IBM,C=GB" -label ibmmqonpremqm

    ```

* Connect to runmqsc and alter the `SSLKEYR` attribute to point to the path of the key repository

    ```bash

    runmqsc
    ALTER QMGR SSLKEYR('/var/mqm/qmgrs/ONPREM_QM/ssl/key')

    ```

### Cloud queue manager 

* Start the command prompt to configure the cloud queue manager using runmqsc.

* Set the environment variables `MQCCDTURL` and `MQSSLKEYR` to the full paths of the downloaded CCDT file and certificate respectively.

   - On Linux/Mac:

     ```bash
        unset MQSERVER
        export MQCCDTURL=<full-path-to-ccdt-file>
        export MQSSLKEYR=<full-path-to-keydb-file>
     ```

   - On Windows:

     ```bash
        unset MQSERVER
        set MQCCDTURL=<full-path-to-ccdt-file>
        set MQSSLKEYR=<full-path-to-keydb-file>
     ```
* Connect to cloud queue manager using *runmqsc*, using your MQ username and platform API key ( The API key is generated under the administration tab when you access the cloud queue manager from the UI. You have to provide the api key when you get a prompt asking for password)

    ```bash
    runmqsc -u myusername -c MyCloudQM
    ```
* Confirm you are successfully connected by executing a command

    ```bash
    runmqsc
    PING QMGR
    ```

* Create the queues in the cloud queue mananger

    ```bash
    DEFINE QLOCAL(TO.ONPREM) USAGE(XMITQ)
    DEFINE QREMOTE(LOCAL) RNAME(LOCAL) RQMNAME(ONPREM_QM) XMITQ(TO.ONPREM)
    DEFINE QLOCAL(LOCAL.REPLY)
    ```
    -  transmit queue that will be used for the cloud sender channel
    -  remote queue definition that allows messages to be addressed to the on-premises queue
    -  local queue that will be used to hold reply messages from the on-premises application 

* Create the channels and authorizations to allow the on-premises queue manager to connect

   - server channel that will respond to the on-prem requester channel

     ```bash
     DEFINE CHANNEL(CLOUD.TO.ONPREM) CHLTYPE(SVR) XMITQ(TO.ONPREM) TRPTYPE(TCP)
     ```

   - receiver channel to accept connections from on-prem sender channel

     ```bash
     DEFINE CHANNEL(ONPREM.TO.CLOUD) CHLTYPE(RCVR) TRPTYPE(TCP)
     ```

* Create the channel authentication record to allow incoming connections from the on-prem QM sender and on-prem QM requester channel

    ```bash
     SET CHLAUTH(ONPREM.TO.CLOUD) TYPE(QMGRMAP) QMNAME(ONPREM_QM) ACTION(ADD) USERSRC(CHANNEL)

     SET CHLAUTH(CLOUD.TO.ONPREM) TYPE(QMGRMAP) QMNAME(ONPREM_QM) ACTION(ADD) USERSRC(CHANNEL)
    ```

## Configuring the TLS security 

* The cloud queue manager is already configured with a default server certificate (a wildcard certificate issued by Let's Encrypt) so you need to download that server certificate to the on-premises machine and configure the queue manager to trust it.

* In the onprem queue manager, change directory into the ‘ssl’ directory for your queue manager. Next, add the cloud public certificate you downloaded earlier. The label should be `ibmmq<qmname>` - where `qmname` is the name of your cloud queue manager ( in lower case ).

    ```bash
    runmqakm -cert -add -db key.kdb -stashed -label ibmmqmycloudqm -file <path_to_cert>\qmgrcert.pem
    ```
* Verify that your certificate is present by running this command:
    ```bash
    runmqakm -cert -list -db key.kdb -stashed
    ```
 
* Set up TLS security by giving the local queue manager the certificates to permit a trust relationship between the two queue managers.

   - on-premises queue manager

     ```bash
     runmqsc
     ALTER CHL('ONPREM.TO.CLOUD') CHLTYPE(SDR) SSLCIPH(ANY_TLS12_OR_HIGHER)

     ALTER CHL('CLOUD.TO.ONPREM') CHLTYPE(RQSTR) SSLCIPH(ANY_TLS12_OR_HIGHER) SSLCAUTH(OPTIONAL)
     ```

  - cloud queue manager

     ```bash
     runmqsc
     ALTER CHL('ONPREM.TO.CLOUD') CHLTYPE(RCVR) SSLCIPH(ANY_TLS12_OR_HIGHER) SSLCAUTH(OPTIONAL)

     ALTER CHL('CLOUD.TO.ONPREM') CHLTYPE(SVR) SSLCIPH(ANY_TLS12_OR_HIGHER) SSLCAUTH(OPTIONAL) 
     ```

## Enabling mutual-authentication TLS security

In this section, you will take the server-authentication TLS enabled channels that you have defined above and alter them to enable mutual authentication between the two queue managers
In order to achieve this, you will need to configure the on-cloud queue manager to “trust” a server certificate that will be presented by the on-premises queue manager and vice-versa.


* If you haven't already created a self signed certificate for the onprem queue manager while setting up the key repository, create one using `runmqakm`. Note that the command should all be on one line and the label should be `ibmmq<qmname>` - where `<qmname>` is the name of your on-premises queue manager in lower case:

    ```bash
    runmqakm -cert -create -db key.kdb -stashed -dn “CN=LOCALQM,O=IBM,C=GB” -label ibmmqonprem_qm
    ```

* extract the public part of the self-signed personal certificate on the on- premises machine by using runmqakm (Note, the command should all be on one line):

    ```bash
    runmqakm -cert -extract -db key.kdb -stashed -label ibmmqonprem_qm -target
    <path_to_download_directory>/onpremcert.pem -format ascii -fips
    ```
* You now need to import the “onpremcert.pem” file into the trusted key store of your on-cloud queue manager
    - In your web browser go to the [IBM Cloud console](https://cloud.ibm.com/resources) and find your MQ service instance.
    - From the list of queue managers, click the row containing your queue manager (MyCloudQM) to go to its details view, and then click on the ‘Trust store’ tab.
    - Click on “Import certificate”, then on “Browse files” and navigate to the onpremcert.pem file you downloaded in the previous steps.
    - Then click “open” and then “next”. Specify the label to give to the certificate (such as “ibmmqonprem_qm”) and then click “Save".

    The newly imported certificate should now appear in the list of certificates in the trust store and it should show as being trusted.

* Return to the runmqsc command prompt that you opened to configure your cloud queue manager ( or open a new prompt if you closed it ).

    - Verify that your connected to the cloud queue manager and apply the `SSLCIPH` and `SSLCAUTH` settings to the existing channels.

        ```bash
        runmqsc
        DISPLAY QMGR QMNAME
        ALTER CHL('ONPREM.TO.CLOUD') CHLTYPE(RCVR) SSLCIPH(ANY_TLS12_OR_HIGHER) SSLCAUTH(REQUIRED)
        ALTER CHL('CLOUD.TO.ONPREM') CHLTYPE(SVR) SSLCIPH(ANY_TLS12_OR_HIGHER) SSLCAUTH(REQUIRED)
        ```
    - Refresh SSL security so that all SSL or TLS channels that are currently running are updated

        ```bash
        REFRESH SECURITY TYPE(SSL)
        ```
* Now you need to do the equivalent steps on the on-premises queue manager. Return to the original command prompt for your on-premises queue manager (or open a new one if you have closed it).

    ```bash
    runmqsc
    DISPLAY QMGR QMNAME
    ALTER CHL('CLOUD.TO.ONPREM') CHLTYPE(RQSTR) SSLCIPH(ANY_TLS12_OR_HIGHER) SSLCAUTH(REQUIRED)
    REFRESH SECURITY TYPE(SSL)
    ```

* You have now finished configuring the channels for mutual authentication TLS.

## Validate the connection

In this section you will start the channels you have defined, confirm that they are running successfully, and send a test message in each direction to prove the flow of messages.

Since the on-premises queue manager has to initiate both its outbound connection to the cloud and also trigger the inbound connection from the cloud (via the on-premises Requester channel) you must start both channels from the on-premises queue manager side.
Return to the runmqsc session for your on-premise queue manager (or create a new one if you have closed the original).

* Check you are attached to the on-premise QM – it should show “ONPREM_QM”

    ```bash
    runmqsc
    DISPLAY QMGR QMNAME
    ```
* Start the sender channel from on-premises to cloud queue manager. 

    ```bash
    START CHANNEL(ONPREM.TO.CLOUD) 
    ```
* Wait for 15 seconds and check that the sender channel shows STATUS(RUNNING)
    ```bash
    DISPLAY CHSTATUS(ONPREM.TO.CLOUD) SSLPEER
    ```
* Start the requester channel on the on-premises queue manager

    ```bash
    START CHANNEL(CLOUD.TO.ONPREM)
    ```
* Wait for 15 seconds and check that the requester channel shows STATUS(RUNNING)
    ```bash
    DISPLAY CHSTATUS(CLOUD.TO.ONPREM) SSLPEER
    ```
Both channels should show STATUS(RUNNING) and in each case, the value
of SSLPEER should match

### Test sending message from cloud to on-premises queue manager

* Return to the command prompt of the onprem queue manager. Check the current queue depth of the local queue is zero, ready for us to test the transmission of messages from cloud to on-premise

    ```bash
    runmqsc
    DISPLAY QSTATUS(LOCAL) CURDEPTH
    ```
    - should show CURDEPTH(0)

* In IBM Cloud, go to your MQ on Cloud service instance, navigate to the your queue manager 'MyCloudQM', and launch the mq console 

* Navigate to the Manage tab in the left navigation panel for queue manager management.
* Click on the Queues tab and locate the remote queue named "LOCAL" from the displayed table. 
* Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") for the queue and then click 'Create message'.
* Write a simple message in the 'Application data' section and then press the 'Create' button.
* Now return to the runmqsc window for the ONPREM_QM, and re-run the command to display the queue depth of the local queue. You will see that the queue depth has increased to 1, indicating that the message was successfully transmitted from the cloud queue manager to the on-premises queue manager.

### Test sending a message from on-premise to Cloud queue manager

You will use the “amqsput” command-line utility to connect to the ONPREM_QM and send a test message which will be transmitted to the cloud queue manager.

* open a new command prompt on your “on-premises” virtual machine and enter the following “amqsput” command to connect to the queue, then type some simple text for your message and press Enter twice (once to finish the message, the second to quit)

    ```bash
    amqsput LOCAL.REPLY ONPREM_QM
    Hello from on-premises
    <enter>
    <enter>
    ```
* Now go back to the MQ Console for your cloud queue manager and click the Refresh icon in the top right corner (two arrows in a circle), to observe that the queue depth for LOCAL.REPLY is now 1 rather than 0.