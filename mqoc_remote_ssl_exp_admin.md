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

# Securing Remote administration using IBM MQ Explorer
{: #mqoc_remote_ssl_exp_admin}

This document guides you on enabling TLS for remote administration of the MQ on cloud queue manager using *MQ Explorer*.

## Prerequisites
{: #mqoc_remote_ssl_exp_admin_prereq}

1. For establishing a secured connection to MQ on Cloud queue manager, you must first setup security on MQ channel. Refer [Configuring MQ Channels with Security](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl)
2. Include Java(jre/bin) to your system path, this is required to be set for using tools such as ikeycmd.

## Tasks on the system that hosts the IBM MQ Explorer
{: #mqoc_remote_ssl_exp_admin_tasks}

1. Create a client key store and copy the public part of queue manager certificate into it:  

    1.1 Create a client key store using the ‘ikeycmd’ tool.
     ```
     ikeycmd -keydb -create -db key -pw <your password> -type jks -expire 0 -stash
     ```
    1.2 Import the Digicert CA certificate into the key store. (**ca.cer** is the queue manager certificate, ensure that fully qualified path of this certificate is given in command line).  
    **Note:** To download the CA certificate, follow the prerequisites topic [here](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#mqoc_chl_ssl_prereq)  
     ```
     ikeycmd -cert -add -db key.jks -file ca.cer -label DigiCertRootCA -stashed -type jks -format ascii
     ```
2. Start the MQ Explorer by running `strmqcfg` command from a command line interface.
3. From the MQ Explorer - Navigator, right click on **Queue Managers** and select **Add Remote Queue Manager** option.
4. In the Queue manager name field, enter the name of the MQ on Cloud queue manager you want to connect to.
5. Ensure that **Connect directly** is selected. Click **Next**.
6. On the **Specify new connection details** page:  
    6.1 In the **Host name or IP address:** field, enter the Hostname of your MQ on Cloud queue manager(gathered from MQ on Cloud queue manager details).  
    6.2 In the **Port number:** field, enter the port number of your MQ on Cloud queue manager(gathered from MQ on Cloud queue manager details).     
    6.3 In the **Server-connection channel** field, enter the value as `CLOUD.ADMIN.SVRCONN`.  
    6.4 Click **Next**.  
7. On the **Specify security exit details** page, Click **Next**.  
8. On the **Specify user identification details** page:  
    8.1 Select the **Enabe user identification** checkbox.  
    8.2 Ensure **User identification compatability mode** is NOT selected.  
    8.3 In the **Userid:** field, type the MQ username gathered from **User permissions** or **Application permissions** of MQ on Cloud Servce.  
    8.4 In the **Password** field, select the **Prompt for passowrd** radio buton.  
    8.5 Click **Next**.  
9. On the **Specify SSL certificate key repository details** page:  
    9.1 Select the **Enable SSL key repositories** checkbox.  
    9.2 Browse and select the key repository created in Step#1 for both **Trusted Certificate Store** and **Personal Certificate Store**.  
    9.3 Click **Next**.  
10. On the **Specify SSL option details** page:  
    10.1 Select the **Enable SSL options** checkbox.  
    10.2 In the **CipherSpec** field, select the value as *"TLS_RSA_WITH_AES_128_CBC_SHA256"* from the dropdown list.  
    10.3 Click **Finish**.  
    10.4 When prompted enter the passwords.  
11. MQ Explorer should now connect to your queue manager for remote administration. All the operations on this queue manager will now run on a secured channel.

## Next step
{: #mqoc_remote_ssl_exp_admin_next}
* [Connect securely from C MQI & JMS application](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_ssl)
