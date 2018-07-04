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

# Configuring MQ Channel with Security
{: #mqoc_configure_chl_ssl}

This page guides you on enabling TLS on MQ channels of an MQ on cloud queue manager, using *CLOUD.ADMIN.SVRCONN* server connection channel, the same
procedure can be followed for other channels.

## Prerequisites

* Please read and get familiarized with the following concepts. This will give an introduction and will also help you setup the configuration that we will use for enabling security.
  - [Configuring administrator access for a queue manager](docs/services/mqcloud/tutorials/tut_mqoc_configure_admin_qm_access.html)
  - [Administering a queue manager using IBM MQ Web Console](docs/services/mqcloud/mqoc_admin_mqweb.html)
  - [Administering a queue manager using IBM MQ Explorer](docs/services/mqcloud/mqoc_admin_mqexp.html)
  - [Administering a queue manager using runmqsc from an IBM MQ client](docs/services/mqcloud/mqoc_admin_mqcli.html)  
  

* Download the public part of the queue manager digital certificate:
  1. [Download the mqoc queue manager digital certificate here](https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt)
  2. Rename the downloaded DigiCertGlobalRootCA.crt as, for example, *ca.cer* and move it to a convenient location.



## Tasks on the MQ on Cloud Queue Manager

Enabling security on MQ channel requires executing set of commands. This can be achieved using any one of the following options:
* MQ Web Console
* MQ Explorer
* RUNMQSC CLI

### Using MQ Web Console
Note: Please ensure that you have carried out the prerequisite steps listed above.

1. Refer to [Login to the MQ web console for your queue manager](https://console.bluemix.net/docs/services/mqcloud/mqoc_admin_mqweb.html#connect_mqoc_admin_mqweb) and perform the steps as listed.
2. On the MQ web console - Refer to **Channels** widget and double click on the channel **CLOUD.ADMIN.SVRCONN**:   
    4.1 In the properties panel, select **SSL**.  
    4.2 In the **SSL CipherSpec:** field, enter the value as `TLS_RSA_WITH_AES_128_CBC_SHA256`.  
    4.3 **Save** & **Close** Properties.  
3. This completes enabling security on an MQ channel. You may now close the MQ web console.

### Using MQ Explorer
Note: Please ensure that you have carried out the prerequisite steps listed above.

1. Refer to [Connect to your queue manager using MQ Explorer](https://console.bluemix.net/docs/services/mqcloud/mqoc_admin_mqexp.html#connect_mqoc_admin_mqexp) and perform the steps as listed.  
2. In the MQ Explorer - Navigator:    
    2.1 Navigate to **Queue Managers**, expand your queue manager and click on **Channels**.  
    2.2 In the **Channels** panel, double click on **CLOUD.ADMIN.SVRCONN**.  
    2.3 In the **CLOUD.ADMIN.SVRCONN** properties pannel, select **SSL**.  
    2.4 In the **SSL Cipher Spec:** field, select `TLS_RSA_WITH_AES_128_CBC_SHA256`.  
    2.5 Click **Apply** and then **OK**.  
3. In the MQ Explorer - Navigator:  
    3.1 Under **Queue Managers**, right click on the queue manager and select **Security -> Refresh SSL**.  
4. This completes enabling security on an MQ channel. You may now disconnect the connection to queue manager by right clicking on queue manager and selecting **Disconnect**.  

### Using RUNMQSC CLI
Note: Please ensure that you have carried out the prerequisite steps listed above.

Enabling security for remote administration using runmqsc-cli will need a corresponding client connection channel to be created. Please use following steps to achieve that:

1. Refer to [Connect to your queue manager using runmqsc](docs/services/mqcloud/mqoc_admin_mqcli.html#connect_mqoc_admin_mqcli) and perform the steps as listed. Please do not exit the runmqsc command shell as the same to be used in steps below.
2. Run following commands to configure the channels:
  ```
  ALTER chl(CLOUD.ADMIN.SVRCONN) chltype(SVRCONN) SSLCAUTH(OPTIONAL)
  ALTER chl(CLOUD.ADMIN.SVRCONN) chltype(SVRCONN) SSLCIPH(TLS_RSA_WITH_AES_128_CBC_SHA256)
  DEFINE CHANNEL(CLOUD.ADMIN.SVRCONN) CHLTYPE(CLNTCONN) CONNAME ('hostname(port)') QMNAME(QMGRNAME) sslciph(TLS_RSA_WITH_AES_128_CBC_SHA256)
  ALTER chl(CLOUD.ADMIN.SVRCONN) chltype(CLNTCONN) sslciph(TLS_RSA_WITH_AES_128_CBC_SHA256)
  end
  ```
3. This completes enabling security on an MQ channel. You may now exit the runmqsc cli.

### You can now follow one of the below links to connect securely for administration

[Configuring security for remote administration using IBM MQ explorer](/docs/services/mqcloud/mqoc_remote_ssl_exp_admin.html)

[Configuring security for remote administration using RUNMQSC CLI](/docs/services/mqcloud/mqoc_remote_ssl_runmqsc_admin.html)

### Securing Application Connections
[Connect securely from MQI C & JMS application](/docs/services/mqcloud/mqoc_connect_app_ssl.html)