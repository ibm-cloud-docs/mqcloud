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

# Securing Remote administration using RUNMQSC CLI
{: #mqoc_remote_ssl_runmqsc_admin}

This document guides on enabling TLS for remote administration of the MQ on Cloud queue manager using *RUNMQSC CLI*

## Prerequisites
1. For establishing a secured connection to MQ on Cloud queue manager, you must first setup security on MQ channel. Refer [Configuring MQ Channels with Security](/docs/services/mqcloud/mqoc_download_logs.html)  
2. Include Java(jre/bin) to your system path, this is required to be set for using tools such as ikeycmd.

### Tasks on the system that hosts the RUNMQSC CLI

1. Create a client key store and copy the public part of queue manager certificate into it:  

    1.1 Create a client key store using the ‘ikeycmd’ tool.
     ```
     ikeycmd -keydb -create -db key -pw <your password> -type kdb -expire 0 -stash
     ``` 
    1.2 Import the Digicert CA certificate into the key store. (**ca.cer** is the Queue manager certificate, ensure that fully qualified path of this certificate is given in command line).
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
    3.1 Open a comand line interface to use in the steps.  
    3.2 Export **MQSSLKEYR** environment variable for the path to the key store. Path should be the full path from the root of the file system to the key store and the key store should be specified with no suffix. For example, for a key store named key.kdb, specify just "key".  
     ```
     For Linux: export MQSSLKEYR="location of clients keystore"
     For Windows: set MQSSLKEYR="location of clients keystore"
     ```
    3.3 Export **MQCHLLIB** environment variable for the path to the channel table file.  
     ```
     For Linux: export MQCHLLIB="location of channel table"
     For Windows: set MQCHLLIB="location of channel table"
     ```
    3.4 Export **MQCHLTAB** environment variable for the name of the channel table file.  
     ```
     For Linux: export MQCHLTAB=AMQCLCHL.TAB
     For Windows: set MQCHLTAB=AMQCLCHL.TAB
     ```
    3.5 Ensure that there is no MQSERVER environment variable set, the host and port will be used from the channel table file.  
4. Run the **runmqsc** administration command specifying the ‘MQ username’ and the queue manager name. When prompted, enter the password( the apikey value).
   ```
   <Path to MQ/bin directory>/runmqsc -c -u <Your MQ Username> <MQoC queue manager name>
   ```

  All the operations on this RUNMQSC will now run on a secured channel.