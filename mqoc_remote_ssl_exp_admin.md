---
copyright:
  years: 2017, 2021
lastupdated: "2021-10-06"

subcollection: mqcloud

keywords: admin, administration, MQ, explorer, SSL, TLS
---

{{site.data.keyword.attribute-definition-list}}

# Securing remote administration using IBM MQ Explorer
{: #mqoc_remote_ssl_exp_admin}

This document covers enabling TLS for remote administration of the MQ on Cloud queue manager using *IBM MQ Explorer*.

## Prerequisites
{: #mqoc_remote_ssl_exp_admin_prereq}

1. If your queue manager is version 9.2.1 revision 1 or older, first set up TLS encryption on the MQ channel. Refer [Enabling TLS security for MQ channels in MQ on Cloud](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl).  If you have a newer queue manager, TLS will already be enabled with the ANY_TLS12_OR_HIGHER cipher.
1. [Download the public certificates](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#download_cert)
1. Create a JKS keystore using [Windows or Linux](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#keystore_jks) or using [Mac OSX](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#keystore_jks_mac)
1. You need access to the MQ client tools for your operating system (for example runmqakm). These are included as part of an MQ server installation on Linux and Windows, or can be installed separately part of the MQ client for Linux or Windows available from the [MQ Downloads](https://ibm.biz/MQdownloads) page, or the [MacOS toolkit for Developers](https://developer.ibm.com/components/ibm-mq/tutorials/mq-macos-dev/)
1. You will need *IBM MQ Explorer* installed in an Eclipse environment on Windows or Linux. Full installation instructions can be
found at [IBM MQ Explorer Installation](https://www.ibm.com/docs/en/ibm-mq/9.2)

## Tasks to perform on the system that hosts the IBM MQ Explorer
{: #mqoc_remote_ssl_exp_admin_tasks}

1. Start the MQ Explorer by running `strmqcfg` command from a command line interface, or clicking the icon.
1. From the MQ Explorer - Navigator, right click on **Queue Managers** and select **Add Remote Queue Manager** option.
1. In the Queue manager name field, enter the name of the MQ on Cloud queue manager you want to connect to.
1. Ensure that **Connect directly** is selected. Click **Next**.
1. On the **Specify new connection details** page:  
    1. In the **Host name or IP address:** field, enter the Hostname of your MQ on Cloud queue manager (gathered from MQ on Cloud queue manager CCDT or text details downloaded earlier).  
    1. In the **Port number:** field, enter the port number of your MQ on Cloud queue manager (gathered from MQ on Cloud queue manager details).     
    1. In the **Server-connection channel** field, enter the value as `CLOUD.ADMIN.SVRCONN`.  
    1. Click **Next**.  
1. On the **Specify security exit details** page, Click **Next**.  
1. On the **Specify user identification details** page:  
    1. Select the **Enable user identification** checkbox.  
    1. Ensure **User identification compatibility mode** is NOT selected.  
    1. In the **Userid:** field, type the MQ username gathered from **User permissions** of the MQ on Cloud Service.  
    1. In the **Password** field, select the **Prompt for password** radio button.  
    1. Click **Next**.  
1. On the **Specify SSL certificate key repository details** page:  
    1. Select the **Enable SSL key repositories** checkbox.  
    1. Browse and select the key repository created in the prereq steps for both **Trusted Certificate Store** and **Personal Certificate Store**.  
    1. Click **Next**.  
1. On the **Specify SSL option details** page:  
    1. Select the **Enable SSL options** checkbox.  
    1. In the **CipherSpec** field, select the value you want, for example *ANY_TLS12_OR_HIGHER* from the dropdown list.  
    1. Click **Finish**.  
    1. When prompted enter the password.  
1. MQ Explorer should now connect to your queue manager for remote administration. All the operations on this queue manager will now run on a secured channel.

## Next step
{: #mqoc_remote_ssl_exp_admin_next}
* [Connect securely from C MQI & JMS application](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_ssl)
