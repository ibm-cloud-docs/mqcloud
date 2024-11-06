---
copyright:
  years: 2017, 2022
lastupdated: "2022-08-25"

subcollection: mqcloud

keywords: secure, client, SSL, TLS, JMS, MQI
---

{{site.data.keyword.attribute-definition-list}}

# Securing application connections in C MQI & JMS programs
{: #mqoc_connect_app_ssl}

This document covers connecting securely to an {{site.data.keyword.mq_short}} queue manager using "C MQI" and "JMS" applications. You will need the application user name and password which you downloaded in the prerequisite steps. You will also need the MQ client for your operating system, which may be part of a full MQ installation, or may be downloaded separately from [here](https://developer.ibm.com/components/ibm-mq/articles/mq-downloads){: external}.

## Prerequisites
{: #mqoc_connect_app_ssl_prereq}

1. For establishing a secured connection to {{site.data.keyword.mq_short}} queue manager, you must first set up TLS encryption on the MQ channel. Refer [Enabling TLS security for MQ channels in {{site.data.keyword.mq_short}}](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl)
2. If you are not familiar with how to connect an application to an {{site.data.keyword.mq_short}} queue manager, there is documentation here:  [Connecting a sample application to a queue manager](https://cloud.ibm.com/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_qm)
3. To use the JSON CCDT definition for your application, you must have a 9.1.2 (or above) installation of the client.


## Tasks specific to the C MQI Program
{: #mqoc_connect_app_ssl_c_tasks}

### Alter the client channel definition table (CCDT)

As part of the prerequisites, you downloaded the JSON CCDT queue manager description earlier. By default, it does not contain the cipher specifications that you associated with the channels, so you have to add that now, adding a transmissionSecurity definition for each channel.

For example:
```json
"channel": [
  {
  "name": "CLOUD.ADMIN.SVRCONN",
  "clientConnection": {
    "connection": [
    {
      "host": "myqueuemanager.qm2.us-south.mq.appdomain.cloud",
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

The cipher specification at the client end has been specified as **SSL_RSA_WITH_AES_128_CBC_SHA256**.  It could be any
TLS 1.2 cipher specification, as the server end was set to accept **ANY_TLS12_OR_HIGHER**.
{: note}

### Export the necessary environment variables

1. Open command line interface and navigate to MQ C Samples directory.
    - The location of this will depend on your operating system - it would be `/var/mqm/Tools/Samples/C` (Linux), `C:\Program Files\IBM\MQ\Tools\c\Samples` (Windows), or on Mac, where you have installed the toolkit, for example `~/mytoolkit/IBM-MQ-Toolkit-Mac-x64-9.1.2.0/samp/bin`.
2. Set the `MQSSLKEYR` environment variable, this is the full path from the system root to the key store file. Note that the filename requires no suffix - so for a key store named key.kdb, specify just "key".
    - For Windows, run `set MQSSLKEYR=c:\mystore\key`
    - For Mac or Linux, `export MQSSLKEYR=/Users/you/store/key`
3. The path to the CCDT file can be set in one of two ways:
    1. Set the environment variable `MQCCDTURL`, this is file path from the system root to the ccdt file to which you added the cipherSpecification earlier.
        - For Windows, run `set MQCCDTURL=c:\mydefinitions\connection_info_ccdt.json`
        - For Mac or Linux, run `export MQCCDTURL=file:///Users/you/definitions/connection_info_ccdt.json`
    2. Set the environment variables `MQCHLLIB` and `MQCHLTAB`. `MQCHLLIB` is the full path to the directory of your ccdt file and `MQCHLTAB` is the filename of the ccdt file to which you added the cipherSpecification earlier.
        - For Windows, run `set MQCHLLIB=c:\mydefinitions` and `set MQCHLTAB=connection_info_ccdt.json`
        - For Mac or Linux, run `export MQCHLLIB=/Users/you/definitions` and `export MQCHLTAB=connection_info_ccdt.json`
4. Set the `MQSAMP_USER_ID` environment variable, this is the user id you would like to connect as. For applications this is the application credential name which you downloaded earlier
    - For Windows, run `set MQSAMP_USER_ID=<yourusername>`
    - For Mac or Linux, `export MQSAMP_USER_ID=<yourusername>`
5. Ensure the `MQSERVER` environment variable is not set by running `unset MQSERVER`
6. Run the sample `amqsputc`, specifying queue name and queue manager name, for example:
    ```bash
    amqsputc DEV.QUEUE.1 QM1
    ```
7. Enter the password for the application credential being used
8. Once the message *'target queue is DEV.QUEUE.1'* appears on command line, it is ready to send messages:
    1. Type the message data/string and when ready press “ENTER” to send the message.
    2. An empty string “ENTER” will end the sample.
9. You can use `amqsgetc` to receive the messages sent.
    ```bash
    amqsgetc DEV.QUEUE.1 <YOURQMGRNAME>
    ```
The C MQI sample program is using a secured connection to send/receive messages.

## Tasks specific to the JMS Program
{: #mqoc_connect_app_ssl_jms_tasks}

If you are not familiar with the JMS sample program, there is a full tutorial on how to install and run the sample without TLS here: https://developer.ibm.com/learningpaths/ibm-mq-badge/write-run-first-mq-app/

The sample above runs on the IBM Java 1.8 SDK on Windows and Linux. At the time of writing, we also tried this using the Oracle 1.8 SDK, but were unable to get the connection working - there was a cipher suite mismatch.
{: important}

When you can run the JMS sample, you now need to alter it to accept the cipher specification:

1. Update the MQ JMS sample for making a secured connection:
    1. Navigate to MQ JMS Samples directory. The location will vary depending on your operating system. By default, these will be $MQ_INSTALLATION_PATH/samp/jms/samples on Linux and %MQ_INSTALLATION_PATH%\tools\jms\samples on Windows
    2. Use any editor to open the *simple/JmsPut.java* program.  
    3. Add following new properties to the jms program, just after creating JMS ConnectionFactory instance.
        ```java
        System.setProperty("javax.net.ssl.keyStore", "/Users/you/store/key.kdb");
        System.setProperty("javax.net.ssl.keyStorePassword", "my_store_password");

        cf.setStringProperty(WMQConstants.USERID, "Your app user ID");
        cf.setStringProperty(WMQConstants.PASSWORD, "Your APIKEY");
        cf.setStringProperty(WMQConstants.WMQ_SSL_CIPHER_SPEC, "ANY_TLS12_OR_HIGHER");
        cf.setStringProperty(WMQConstants.WMQ_CHANNEL, "CLOUD.APP.SVRCONN");
        cf.setIntProperty(WMQConstants.WMQ_CONNECTION_MODE, WMQConstants.WMQ_CM_CLIENT);
        ```
        - The property keyStore should be the full path to the keystore which you created in [Enabling TLS security for MQ channels in {{site.data.keyword.mq_short}}](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#mqoc_chl_ssl_keystore)
        - The cipher specification at the client end could be any TLS 1.2 specification, but it is recommended that you set this to **ANY_TLS12_OR_HIGHER**.
    4. Find the values for hostname, port, and queue manager properties gathered from {{site.data.keyword.mq_short}} queue manager details and set them in the JMS program as shown below:
        ```java
        cf.setStringProperty(WMQConstants.WMQ_HOST_NAME, "Your_Queue_Manager_Host_Name_From_CCDT");
        cf.setIntProperty(WMQConstants.WMQ_PORT, "10305");
        cf.setStringProperty(WMQConstants.WMQ_QUEUE_MANAGER, "Your_Queue_Manager_Name_From_CCDT");
        ```
    5. Save and Close the editor.
2. Compile and Run the JMS Sample:    
    1. Open a command line interface to use in the steps.  
    2. If you have not already done this - update System class path to include MQ JMS jars and JMS samples class folder.  
        ```text
        On Linux:
        export CLASSPATH=$MQ_INSTALLATION_PATH/java/lib/com.ibm.mqjms.jar:$MQ_INSTALLATION_PATH/samp/jms/samples:

        On Windows:
        Set CLASSPATH=%MQ_INSTALLATION_PATH%\java\lib\com.ibm.mqjms.jar;%MQ_INSTALLATION_PATH%\tools\jms\samples;
        ```
    3. Navigate to $MQ_INSTALLATION_PATH/samp/jms/samples and run `javac simple/JmsPut.java`  
    4. Run the JMS Program `java simple/JmsPut`  

This JMS Program sends and receives a message using a secured connection. The output should look like this:

```text
  root@d93d60e4f179:/# java -cp ./com.ibm.mq.allclient-9.0.4.0.jar:./javax.jms-api-2.0.1.jar:. com.ibm.mq.samples.jms.JmsPutGet
  Sent message:

  JMSMessage class: jms_text
  JMSType:          null
  JMSDeliveryMode:  2
  JMSDeliveryDelay: 0
  JMSDeliveryTime:  1563884375664
  JMSExpiration:    0
  JMSPriority:      4
  JMSMessageID:     ID:414d51204d515f65735f663920202020806f355d04ff4924
  JMSTimestamp:     1563884375664
  JMSCorrelationID: null
  JMSDestination:   queue:///DEV.QUEUE.1
  JMSReplyTo:       null
  JMSRedelivered:   false
  JMSXAppID: JmsPutGet (JMS)             
  JMSXDeliveryCount: 0
  JMSXUserID: app1        
  JMS_IBM_PutApplType: 28
  JMS_IBM_PutDate: 20190723
  JMS_IBM_PutTime: 12193624
  Your lucky number today is 633

  Received message:
  Your lucky number today is 633
  SUCCESS
```
