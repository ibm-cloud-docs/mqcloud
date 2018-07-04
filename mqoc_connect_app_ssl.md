---
copyright:
  years: 2017, 2018
lastupdated: "2018-07-02"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing application connections in C MQI & JMS programs
{: #mqoc_connect_app_ssl}

This document guides to connect securely to an MQ on Cloud queue manager using "C MQI" and "JMS" applications.

## Prerequisites
1. For establishing a secured connection to MQ on Cloud queue manager, you must first setup security on MQ channel. Refer [Configuring MQ Channels with Security](/docs/services/mqcloud/mqoc_download_logs.html)
2. Please read and familiarize with the concepts discussed at following link  [Connecting a sample application to a queue manager](https://console.bluemix.net/docs/services/mqcloud/mqoc_connect_app_qm.html#mqoc_connect_app_qm)
3. Include Java(jre/bin) to your system path. The path is required to be set for using tools such as ikeycmd.

## Tasks on the system that runs C MQI Program
1. Create a client key store and copy the public part of queue manager certificate into it.  

    1.1 Create a client key store using the ‘ikeycmd’ tool.
     ```
     ikeycmd -keydb -create -db key -pw <your password> -type kdb -expire 0 -stash
     ``` 
    1.2 Import the Digicert CA certificate into the key store. (**ca.cer** is the queue manager certificate, ensure that fully qualified path of this certificate is given in command line).
     ```
     ikeycmd -cert -add -db key.kdb -file ca.cer -label DigiCertRootCA -stashed -type kdb -format ascii
     ```

2. Download the channel definition table for the client:  
    2.1 To obtain the CCDT file, we need to download the diagnostic data for the queue manager.  
    2.2 On the Queue Manager dialogue page on MQ on Cloud, select the **Logs and Diagnostics** tab.  
    2.3 Click on the **Collect diagnostics**.  
    2.4 Specify a password of your choice and confirm, then click on the **Collect logs**.  
    2.5 Once the collection has completed, this would take few minutes to complete. Click on the **Download zip** file link.  
    2.6 Open the zip file specifying the password when prompted, and navigate to the /var/mqm/qmgrs/qmgr_name/@ipcc directory.  
    2.7 Copy the **AMQCLCHL.TAB** file to a convenient location.  

3. Setting up security for RUNMQSC CLI:  
    3.1 Open command line interface and navigate to MQ C Samples directory.
     ```
     On Linux: /var/mqm/Tools/Samples/C/ 
     On Windows: C:\Program Files\IBM\MQ\Tools\c\Samples
     ``` 
    3.2 Export **MQSSLKEYR** environment variable for the path to the key store. Path should be the full path from the root of the file system to the key store and the key store should be specified with no suffix. For example, for a key store named key.kdb, specify just "key".  
     ```
     On Linux: export MQSSLKEYR="location of clients keystore"
     On Windows: set MQSSLKEYR="location of clients keystore"
     ```
    3.3 Export **MQCHLLIB** environment variable for the path to the channel table file.  
     ```
     On Linux: export MQCHLLIB="location of channel table"
     On Windows: set MQCHLLIB="location of channel table"
     ```
    3.4 Export **MQCHLTAB** environment variable for the name of the channel table file.  
     ```
     On Linux: export MQCHLTAB=AMQCLCHL.TAB
     On Windows: set MQCHLTAB=AMQCLCHL.TAB
     ```
    3.5 Export the **MQSAMP_USER_ID** environment variable. Specify the MQ username gathered from the **User permissions** or **Application permissions** of the MQ on Cloud Service.
     ```
     On Linux: export MQSAMP_USER_ID="<MQ Username>"
     On Windows: set MQSAMP_USER_ID=<MQ Username>
     ```
    3.6 Ensure that there is no MQSERVER environment variable set, the host and port will be used from the channel table file.  

4. Run the sample **amqsputc**, specifying queue name and the queue manager name, for example:
   ```
   amqsputc DEV.QUEUE.1 <QMGRNAME>
   ```

5. When prompted enter the password for MQ username specified.

6. Once the message *'target queue is DEV.QUEUE.1'* appears on command line, its ready to send messages:  
    6.1 Type the message data/string and when ready press “ENTER” to send the message.  
    6.2 An empty string “ENTER” will end the sample.  

7. You can use **amqsgetc** to receive the messages sent.
   ```
   amqsgetc DEV.QUEUE.1 <QMGRNAME>
   ```
This C MQI sample programs use secured connection to send/receive messages.

## Tasks on the system that runs JMS Program

1. Create a client key store and copy the public part of queue manager certificate into it:  

    1.1 Create a client key store using the ‘ikeycmd’ tool.
     ```
     ikeycmd -keydb -create -db key -pw <your password> -type jks -expire 0 -stash
     ``` 
    1.2 Import the Digicert CA certificate into the key store. (**ca.cer** is the queue manager certificate, ensure that fully qualified path of this certificate is given in command line).
     ```
     ikeycmd -cert -add -db key.jks -file ca.cer -label DigiCertRootCA -stashed -type jks -format ascii
     ```
2. Update the MQ JMS sample for making a secured connection:  
    2.1 Navigate to MQ JMS Samples directory.  
      ```
       On Linux: MQ_INSTALLATION_PATH/samp/jms/samples
       On Windows: MQ_INSTALLATION_PATH\tools\jms\samples
      ```
    2.2 Use any editor to open the *simple/SimplePTP.java* program.  
    2.3 Add following new properties to the jms program, just after creating JMS ConnectionFactory instance.
      ```
      System.setProperty("javax.net.ssl.keyStore", <path to key repository> );
      System.setProperty("javax.net.ssl.keyStorePassword", <key repository password> );
      
      cf.setStringProperty(WMQConstants.WMQ_SSL_CIPHER_SPEC,"SSL_RSA_WITH_AES_128_CBC_SHA256");
      cf.setStringProperty(WMQConstants.WMQ_CHANNEL, "CLOUD.ADMIN.SVRCONN");
      cf.setIntProperty(WMQConstants.WMQ_CONNECTION_MODE, WMQConstants.WMQ_CM_CLIENT);
      ```
    2.4 Gather the values of Hostname, Port, and QueueManager properties from MQ on Cloud QueueManager details and set them in the JMS program as shown below:
    ```
      cf.setStringProperty(WMQConstants.WMQ_HOST_NAME, "MQ on Cloud queue manager hostname");
      cf.setIntProperty(WMQConstants.WMQ_PORT, "MQ on Cloud queue manager port");
      cf.setStringProperty(WMQConstants.WMQ_QUEUE_MANAGER, "MQ on Cloud queue manager name");
    ```
    2.5 Modify the *cf.createConnection()* to pass MQ Username and password gathered from the **User permissions** or **Application permissions** of the MQ on Cloud Service.
      ```
      connection = cf.createConnection(<Your MQ username>, <password(apikey)>);
      ```
    2.6 Save and Close the editor.  
    
3. Compile and Run the JMS Sample:    
    3.1 Open a command line interface to use in the steps.  
    3.2 Include Java JDK(jdk/bin) in path.  
    3.3 Update System class path to include MQ JMS jars and JMS samples class folder.  
    ```
    On Linux: 
    export CLASSPATH=MQ_INSTALLATION_PATH/java/lib/com.ibm.mqjms.jar:MQ_INSTALLATION_PATH/samp/jms/samples:

    On Windows: 
    Set CLASSPATH=MQ_INSTALLATION_PATH\java\lib\com.ibm.mqjms.jar;MQ_INSTALLATION_PATH\tools\jms\samples;
    ```
    3.4 Navigate to MQ_INSTALLATION_PATH/samp/jms/samples and run following command:  
    `javac simple/SimplePTP.java`  
    3.5 Run the JMS Program.  
    `java simple/SimplePTP`  

  This JMS Program sends and receives a message using secured connection.