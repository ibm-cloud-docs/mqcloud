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

# Securing remote administration using IBM MQ Explorer
{: #mqoc_remote_ssl_exp_admin}

This document covers enabling TLS for remote administration of the MQ on Cloud queue manager using *IBM MQ Explorer*.

## Prerequisites
{: #mqoc_remote_ssl_exp_admin_prereq}

1. For establishing a secured connection to MQ on Cloud queue manager, you must first set up TLS encryption on the MQ channel. Refer [Enabling TLS security for MQ channels in MQ on Cloud](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl)
2. You need access to the MQ client tools for your operating system (for example runmqakm). These are included as part of an MQ server installation on Linux and Windows, or can be installed separately part of the MQ client for Linux or Windows available from the [MQ Downloads](https://ibm.biz/MQdownloads) page, or the [MacOS toolkit for Developers](https://developer.ibm.com/messaging/2019/02/05/ibm-mq-macos-toolkit-for-developers/)

## Tasks to perform on the system that hosts the IBM MQ Explorer
{: #mqoc_remote_ssl_exp_admin_tasks}

1. Start the MQ Explorer by running `strmqcfg` command from a command line interface, or clicking the icon.
2. From the MQ Explorer - Navigator, right click on **Queue Managers** and select **Add Remote Queue Manager** option.
3. In the Queue manager name field, enter the name of the MQ on Cloud queue manager you want to connect to.
4. Ensure that **Connect directly** is selected. Click **Next**.
5. On the **Specify new connection details** page:  
    5.1 In the **Host name or IP address:** field, enter the Hostname of your MQ on Cloud queue manager (gathered from MQ on Cloud queue manager CCDT or text details downloaded earlier).  
    5.2 In the **Port number:** field, enter the port number of your MQ on Cloud queue manager (gathered from MQ on Cloud queue manager details).     
    5.3 In the **Server-connection channel** field, enter the value as `CLOUD.ADMIN.SVRCONN`.  
    5.4 Click **Next**.  
6. On the **Specify security exit details** page, Click **Next**.  
7. On the **Specify user identification details** page:  
    7.1 Select the **Enable user identification** checkbox.  
    7.2 Ensure **User identification compatibility mode** is NOT selected.  
    7.3 In the **Userid:** field, type the MQ username gathered from **User permissions** of the MQ on Cloud Service.  
    7.4 In the **Password** field, select the **Prompt for password** radio button.  
    7.5 Click **Next**.  
8. On the **Specify SSL certificate key repository details** page:  
    8.1 Select the **Enable SSL key repositories** checkbox.  
    8.2 Browse and select the key repository created in Step#1 for both **Trusted Certificate Store** and **Personal Certificate Store**.  
    8.3 Click **Next**.  
9. On the **Specify SSL option details** page:  
    9.1 Select the **Enable SSL options** checkbox.  
    9.2 In the **CipherSpec** field, select the value you want, for example *ANY_TLS12* from the dropdown list.  
    9.3 Click **Finish**.  
    9.4 When prompted enter the password.  
10. MQ Explorer should now connect to your queue manager for remote administration. All the operations on this queue manager will now run on a secured channel.

## Next step
{: #mqoc_remote_ssl_exp_admin_next}
* [Connect securely from C MQI & JMS application](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_ssl)
