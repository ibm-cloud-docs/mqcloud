---
copyright:
  years: 2017, 2019
lastupdated: "2018-07-06"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing remote administration using runmqsc
{: #mqoc_remote_ssl_runmqsc_admin}

This document describes the process of enabling TLS for remote administration of the MQ on Cloud queue manager using the *runmqsc command line interface*

## Prerequisites
{: #mqoc_remote_ssl_runmqsc_admin_prereq}

1. For establishing a secured connection to MQ on Cloud queue manager, you must first setup security on MQ channel. Refer [Enabling TLS security for MQ channels in MQ on Cloud](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl)  
2. To gain access to tools such as runmqakm, you need either a full installation of MQ, or a client for your operating system from the downloads page here: https://developer.ibm.com/messaging/mq-downloads/.  There is also a new client for MacOS here:
https://developer.ibm.com/messaging/2019/02/05/ibm-mq-macos-toolkit-for-developers/

## Tasks on the system that hosts runmqsc
{: #mqoc_remote_ssl_runmqsc_admin_tasks}


1. Alter the channel definition table for the client:

  You downloaded the CCDT queue manager description earlier. It does not contain the cipher specifications that you associated with
  the channels, so you have to add that now, adding a transmissionSecurity definition for each channel.

  For example:




```
         "channel": [
          {
           "name": "CLOUD.ADMIN.SVRCONN",
           "clientConnection": {
             "connection": [
             {
              "host": "myqueuemanager.mq.test.cloud.ibm.com",
              "port": 31500
             }
             ],
             "queueManager": "MQ_TEST_ONE"
           },
           "transmissionSecurity": {
             "cipherSpecification": "SSL_RSA_WITH_AES_128_CBC_SHA256",
           },
           "type": "clientConnection"
          },

```


  **Note** The cipher specification at the client end has been specified as **SSL_RSA_WITH_AES_128_CBC_SHA256**.  It could be any
     TLS 1.2 cipher specification, as the server end was set to accept **ANY_TLS12**.



2. Export environment variables.

  2.1 Open command line interface and navigate to MQ C Samples directory. The location of this will depend on your operating system - it would
      be /var/mqm/Tools/Samples/C (Linux), C:\Program Files\IBM\MQ\Tools\c\Samples (Windows), or on Mac, where you have installed the toolkit, for
      example ~/mytoolkit/IBM-MQ-Toolkit-Mac-x64-9.1.2.0/samp/bin.

      2.2 Set the following environment variables, using "set" on Windows, or "export" on Mac/Linux.

  MQSSLKEYR is the full path from the system root to the key store file. Note that the filename requires no suffix - so for a key store named key.kdb, specify just "key".  

```
    export MQSSLKEYR=/Users/you/store/key
    set MQSSLKEYR=c:\mystore\key
```

  MQCHLTAB is the full path from the system root to the ccdt file to which you added the cipherSpecification earlier.

```
    export MQCHLTAB=/Users/you/definitions/connection_info_ccdt.json
    set MQCHLTAB=c:\mydefinitions\connection_info_ccdt.json
```

  2.3 Ensure that there is no MQSERVER environment variable set, the host and port will be used from the channel table file.  

3. Run the **runmqsc** administration command specifying the ‘MQ username’ and the queue manager name. These are your own user credentials you
downloaded earlier.
 When prompted, enter the password - this is the  user api key that you downloaded earlier  (Note: Your user api key, not the application api key).
   ```
   <Path to MQ/bin directory>/runmqsc -c -u <Your MQ Username> <MQoC queue manager name>
   ```
  All the operations on this runmqsc will now run on a secured channel.

## Next step
{: #mqoc_remote_ssl_runmqsc_admin_next}

* [Connect securely from C MQI & JMS application](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_ssl)
