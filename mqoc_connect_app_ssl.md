---
copyright:
  years: 2017, 2020
lastupdated: "2018-07-06"

subcollection: mqcloud

keywords: secure, client, SSL, TLS, JMS, MQI
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing application connections in C MQI & JMS programs
{: #mqoc_connect_app_ssl}

This document covers connecting securely to an MQ on Cloud queue manager using "C MQI" and "JMS" applications. You will need the application user name and
password which you downloaded in the prerequisite steps. You will also need the MQ client for your operating system, which
may be part of a full MQ installation, or may be downloaded separately from here: https://developer.ibm.com/components/ibm-mq/articles/mq-downloads

## Prerequisites
{: #mqoc_connect_app_ssl_prereq}

1. For establishing a secured connection to MQ on Cloud queue manager, you must first set up TLS encryption on the MQ channel. Refer [Enabling TLS security for MQ channels in MQ on Cloud](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl)
2. If you are not familiar with how to connect an application to an MQ on Cloud queue manager, there is documentation here:  [Connecting a sample application to a queue manager](https://cloud.ibm.com/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_qm)
3. To use the JSON CCDT definition for your application, you must have a 9.1.2 (or above) installation of the client.


## Tasks specific to the C MQI Program
{: #mqoc_connect_app_ssl_c_tasks}

1. Alter the channel definition table for the client:  
    You downloaded the JSON CCDT queue manager description earlier. By default, it does not contain the cipher specifications that you associated with
    the channels, so you have to add that now, adding a transmissionSecurity definition for each channel.

    For example:

    ```
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

  **Note** The cipher specification at the client end has been specified as **SSL_RSA_WITH_AES_128_CBC_SHA256**.  It could be any
TLS 1.2 cipher specification, as the server end was set to accept **ANY_TLS12_OR_HIGHER**.


2. Export environment variables:  
    2.1 Open command line interface and navigate to MQ C Samples directory. The location of this will depend on your operating system - it would
    be /var/mqm/Tools/Samples/C (Linux), C:\Program Files\IBM\MQ\Tools\c\Samples (Windows), or on Mac, where you have installed the toolkit, for
    example ~/mytoolkit/IBM-MQ-Toolkit-Mac-x64-9.1.2.0/samp/bin.

    2.2 Set the following environment variables, using "set" on Windows, or "export" on Mac/Linux:

      **MQSSLKEYR** is the full path from the system root to the key store file. Note that the filename requires no suffix - so for a key store named key.kdb, specify just "key".

      ```
      export MQSSLKEYR=/Users/you/store/key
      set MQSSLKEYR=c:\mystore\key
      ```

      **MQCCDTURL** is the file path from the system root to the ccdt file to which you added the cipherSpecification earlier.

      ```
      export MQCCDTURL=file:////Users/you/definitions/connection_info_ccdt.json
      set MQCCDTURL=file:///c:/mydefinitions/connection_info_ccdt.json
      ```

      **Note** There are two different means of identifying your CCDT file, if the above does not work, try the following two environment variables:

      **MQCHLLIB** is the full path to the directory of your ccdt file.

      ```
      export MQCHLLIB=/Users/you/definitions
      set MQCHLTAB=c:\mydefinitions
      ```

      **MQCHLTAB** is the filename of the ccdt file to which you added the cipherSpecification earlier.

      ```
      export MQCHLTAB=connection_info_ccdt.json
      set MQCHLTAB=connection_info_ccdt.json
      ```

      **MQSAMP_USER_ID** is the user id. For applications this is the application id which you downloaded earlier.

      ```
      export MQSAMP_USER_ID=yourusername
      set MQSAMP_USER_ID=yourusername
      ```

    2.3 Ensure that there is no **MQSERVER** environment variable set, the host and port will be used from the channel table file.

    ```
    unset MQSERVER
    ```


3. Run the sample **amqsputc**, specifying queue name and the queue manager name, for example:

   ```
   amqsputc DEV.QUEUE.1 <YOURQMGRNAME>
   ```

4. When prompted enter the password for application username specified.

5. Once the message *'target queue is DEV.QUEUE.1'* appears on command line, it is ready to send messages:  
    5.1 Type the message data/string and when ready press “ENTER” to send the message.  
    5.2 An empty string “ENTER” will end the sample.  

6. You can use **amqsgetc** to receive the messages sent.
   ```
   amqsgetc DEV.QUEUE.1 <YOURQMGRNAME>
   ```
The C MQI sample program is using a secured connection to send/receive messages.


## Tasks specific to the JMS Program
{: #mqoc_connect_app_ssl_jms_tasks}

If you are not familiar with the JMS sample program, there is a full tutorial on how to install and run the
sample without TLS here: https://developer.ibm.com/messaging/learn-mq/mq-tutorials/develop-mq-jms/

**Note**  The sample above runs on the IBM Java 1.8 SDK on Windows and Linux. At the time of writing, we also tried this
using the Oracle 1.8 SDK, but were unable to get the connection working - there was a cipher suite mismatch.

When you can run the JMS sample, you now need to alter it to accept the cipher specification:

1. Update the MQ JMS sample for making a secured connection:

    1.1 Navigate to MQ JMS Samples directory. The location will vary depending on your operating system. By default, these will be $MQ_INSTALLATION_PATH/samp/jms/samples on Linux and %MQ_INSTALLATION_PATH%\tools\jms\samples on Windows

    1.2 Use any editor to open the *simple/SimplePTP.java* program.  
    1.3 Add following new properties to the jms program, just after creating JMS ConnectionFactory instance.
      ```
      System.setProperty("javax.net.ssl.keyStore", ""/Users/you/store/key.kdb" );
      System.setProperty("javax.net.ssl.keyStorePassword", "my_store_password" );

      cf.setStringProperty(WMQConstants.WMQ_SSL_CIPHER_SPEC,"SSL_RSA_WITH_AES_128_CBC_SHA256");
      cf.setStringProperty(WMQConstants.WMQ_CHANNEL, "CLOUD.APP.SVRCONN");
      cf.setIntProperty(WMQConstants.WMQ_CONNECTION_MODE, WMQConstants.WMQ_CM_CLIENT);
      ```
    1.4 Find the values for hostname, port, and queue manager properties gathered from MQ on Cloud queue manager details and set them in the JMS program as shown below:
    ```
      cf.setStringProperty(WMQConstants.WMQ_HOST_NAME, "Your_Queue_Manager_Host_Name_From_CCDT");
      cf.setIntProperty(WMQConstants.WMQ_PORT, "10305");
      cf.setStringProperty(WMQConstants.WMQ_QUEUE_MANAGER, "Your_Queue_Manager_Name_From_CCDT");
    ```

    1.5 Save and Close the editor.  

**Note** The property keyStore is the full path to the keystore which you created in
[Enabling TLS security for MQ channels in MQ on Cloud](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#mqoc_chl_ssl_keystore)

**Note** The cipher specification at the client end has been specified as **SSL_RSA_WITH_AES_128_CBC_SHA256**.  It could be any
TLS 1.2 cipher specification, as the server end was set to accept **ANY_TLS12_OR_HIGHER**.

2. Compile and Run the JMS Sample:    
    2.1 Open a command line interface to use in the steps.  
    2.2 If you have not already done this - update System class path to include MQ JMS jars and JMS samples class folder.  
    ```
    On Linux:
    export CLASSPATH=$MQ_INSTALLATION_PATH/java/lib/com.ibm.mqjms.jar:$MQ_INSTALLATION_PATH/samp/jms/samples:

    On Windows:
    Set CLASSPATH=%MQ_INSTALLATION_PATH%\java\lib\com.ibm.mqjms.jar;%MQ_INSTALLATION_PATH%\tools\jms\samples;
    ```
    2.3 Navigate to $MQ_INSTALLATION_PATH/samp/jms/samples and run following command:  
    `javac simple/SimplePTP.java`  

    2.4 Run the JMS Program.  
    `java simple/SimplePTP`  

  This JMS Program sends and receives a message using a secured connection. The output should look like this:

  ```
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
