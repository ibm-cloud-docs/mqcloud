---
copyright:
  years: 2017, 2019
lastupdated: "2019-12-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Enabling TLS security for MQ channels in MQ on Cloud
{: #mqoc_configure_chl_ssl}

The administration and application channels in your MQ on Cloud queue manager are configured by default without TLS security. Enabling TLS causes
the administration or application connections to encrypt the conversation thus protecting sensitive data and credentials.

To achieve TLS encryption, firstly the MQ on Cloud channels need to be given an agreed SSL cipher spec. Secondly, the application or administration
software needs to trust a public certificate for the MQ on Cloud queue manager certificate. This can be the issuer certificate, or the individual queue manager certificate. Both are available for download from the MQ on Cloud service console.

You will need to gather some data from your MQ on Cloud queue instance:

1. The administration user's username and password.
2. An application user's username and password.
3. The certificate chain ending in the queue manager certificate, starting from the root CA certificate.
4. The description of the queue manager formatted in JSON (called CCDT data).

The following paragraphs will guide you through gathering the data from the MQ on Cloud console, and will also guide you through the process of
altering the administration and application channels to apply TLS security.  Subsequent pages linked from the end of this document will show you
how to remotely administer using TLS, and also how to connect the C and JMS MQ samples to the queue manager.

The following description will be altering the CLOUD.ADMIN.SVRCONN channel - this will allow the administrator to connect securely.
Similarly, we will alter the CLOUD.APP.SVRCONN channel, which will be used by applications such as the C or JMS samples.

**Note** You will need access to the MQ tools for your operating system (for example runmqakm). These are part of an MQ installation on Linux and Windows, and have recently been made available in the [MacOS toolkit for Developers](https://developer.ibm.com/messaging/2019/02/05/ibm-mq-macos-toolkit-for-developers/). They can also be downloaded as a separate MQ Client from the [MQ Downloads](https://ibm.biz/MQdownloads) page.

## Reference Documentation
{: #mqoc_chl_ssl_prereq}

* The following links provide a handy reference for information on how to administer an MQ on Cloud queue manager using the standard administration tools. You may choose your preferred tool and follow the instructions in this document.

  - [Configuring administrator access for a queue manager](/docs/services/mqcloud?topic=mqcloud-tut_mqoc_configure_admin_qm_access)
  - [Administering a queue manager using IBM MQ Web Console](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqweb)
  - [Administering a queue manager using IBM MQ Explorer](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqexp)
  - [Administering a queue manager using runmqsc from an IBM MQ client](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqcli)  


## Tasks on the MQ on Cloud queue manager
{: #mqoc_chl_ssl_tasks}

As mentioned earlier, enabling security on an MQ channel requires configuring a cipher spec, and exchanging public certificates between the queue manager and the client (and for Mutual TLS, also between the client and the queue manager). The configuration of the
cipher spec may be done using any of the three standard MQ administration tools. The method for each is described below, so pick your
preferred tool and follow the instructions. For access to the user credentials and certificate, the MQ on Cloud service console is required.

### Using the MQ on Cloud service console to gather credentials and certificates

1. Open the MQ on Cloud service console and locate your queue manager.

2. Gather the queue manager certificate from the Key store
To enable the client process to trust the queue manager we must download the public certificate that will be presented by the queue manager.

Click on the **Key store** tab, and identify the certificate that is marked as "In use: Queue manager" (by default this is **qmgrcert_yyyymm**). Download the public certificate by opening the **...** menu in the certificate, and selecting **Download public certificate**. The download will give you a PEM file (e.g. qmgrcert_yyyymm.pem) which you should save in a known location on your local machine. The downloaded file includes the full trust chain including the leaf certificate that is presented by the queue manager, and any certificate authority (CA) certs that were used to issue that leaf certificate.

![Image showing downloading the leaf certificate](./images/mqoc_tls_leaf_download.png)

3. Gather the admin user's credentials
When you first select the **Administration** tab for your queue manager, your user will be given permissions as the administrator. You should note the user name, and follow the steps to download the API key (which is the password you will use to connect later).

4. Create an application user for the JMS and C applications
Select the **Application credentials** tab for your queue manager, and follow the process to add a new application credentials. Save the
generated API key, which is the password for applications to connect with.

5. Download the JSON CCDT description of your queue manager
Click the **Connection Info** button, and follow the instructions to download the CCDT form of the connection info. You might also want to download the text
version, which is easier to read, and a useful source of the queue manager name and url.

The CCDT file downloaded should look like this:

```
{
 "channel": [
  {
   "name": "CLOUD.ADMIN.SVRCONN",
   "clientConnection": {
     "connection": [
     {
      "host": "myhost.cloud.ibm.com",
      "port": 31605
     }
     ],
     "queueManager": "MQ_ONE"
   }
  },
  {
   "name": "CLOUD.APP.SVRCONN",
   "clientConnection": {
    "connection": [
     {
      "host": "myhost.cloud.ibm.com",
      "port": 31605
     }
    ],
    "queueManager": "MQ_ONE"
   },
   "type": "clientConnection"
  }
 ]
}

```

The following sections describe how to configure the channels to apply TLS security using the MQ Console, MQ Explorer and runmqsc.

### Using MQ Console to alter the channels

1. Refer to [Login to the MQ Web Console for your queue manager](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqweb#connect_mqoc_admin_mqweb) and perform the steps to open an MQ web console attached to your MQ on Cloud queue manager.

2. Alter the channels to expect TLS security.

    2.1 In the MQ Web Console **Channels** widget - double click on the channel **CLOUD.ADMIN.SVRCONN**  

    2.2 In the properties panel, select **SSL**.

    2.3 In the **SSL CipherSpec:** field, enter a value, for example `ANY_TLS12`.  This is not a list, so if you want to choose another cipher spec,
please refer to the IBM MQ documentation for [Enabling CipherSpecs](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.1.0/com.ibm.mq.sec.doc/q014260_.htm)

    2.4 **Save** & **Close** Properties.

![Image showing downloading the SSL cipher spec in MQ Web Console](./images/mqoc_tls_ssl_mq_console.png)


3. Repeat the above for the **CLOUD.APP.SVRCONN** channel.

4. In the **Queue Managers** widget, select your queue manager, and from the **...** dropdown menu, select **Refresh Security...**. Within the panel, select **SSL**
5. The Cipher spec is now configured, if you no longer need the MQ Web Console you can log out.

### Using MQ Explorer to alter the channels

1. Refer to [Connect to your queue manager using MQ Explorer](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqexp#connect_mqoc_admin_mqexp) and perform the steps to connect an MQ Explorer to your MQ on Cloud queue manager.

2. In the MQ Explorer - Navigator:    
    2.1 Navigate to **Queue Managers**, expand your queue manager and click on **Channels**.  
    2.2 In the **Channels** panel, double click on **CLOUD.ADMIN.SVRCONN**.  
    2.3 In the **CLOUD.ADMIN.SVRCONN** properties pannel, select **SSL**.  
    2.4 In the **SSL Cipher Spec:** field, select your cipher spec, for example `ANY_TLS12`.  
    2.5 Click **Apply** and then **OK**.  
3. Repeat the above for the channel **CLOUD.APP.SVRCONN**

![Image showing SSL spec in MQ Explorer](./images/mqoc_tls_ssl_mq_explorer.png)

4. Under **Queue Managers**, right click on the queue manager and select **Security -> Refresh SSL**.  

5. This completes enabling TLS encryption on the MQ channels. If you no longer need the MQ Explorer, you can disconnect the connection to queue manager by right clicking on queue manager and selecting **Disconnect**.  

### Using the runmqsc command line to alter the channels


1. Refer to [Connect to your queue manager using runmqsc](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqcli#connect_mqoc_admin_mqcli) and perform the steps to
connect to your MQ on Cloud queue manager. Do not exit the runmqsc command shell as is will be used in steps below.

2. Run following commands to configure the channels:

Note: Here we are setting the channel authentication to optional. This is configuring one-way TLS. If mutual TLS is required, then set the SSLCAUTH to REQUIRED, and use the MQ on Cloud web console **Trust Store** tab to upload the public key from your local application.

  ```
  ALTER CHANNEL(CLOUD.ADMIN.SVRCONN) CHLTYPE(SVRCONN) SSLCAUTH(OPTIONAL) SSLCIPH(ANY_TLS12)
  ALTER CHANNEL(CLOUD.APP.SVRCONN) CHLTYPE(SVRCONN) SSLCAUTH(OPTIONAL) SSLCIPH(ANY_TLS12)
  REFRESH SECURITY TYPE(SSL)
  end
  ```
3. This completes enabling TLS encryption on the MQ channels. If you no longer need the runmqsc cli, you can exit now.

## Create a Keystore file
{: #mqoc_chl_ssl_keystore}

All the following pages require that you have a keystore with the certificates you downloaded
in it. The following steps can be used to create that keystore.

1. Create a client key store and copy the public part of queue manager certificate chain into it.  

    1.1 Create a client key store using the ‘runmqakm’ tool.
     ```
     runmqakm -keydb -create -db key.kdb -pw <your password> -type pkcs12 -expire 0 -stash

     # In some operating systems you may have to update the file permissions to make the keystore readable
     chmod +rw key.*
     ```
    1.2 Import the queue manager certificate into the key store (this is the **qmgrcert** you downloaded from the MQ on Cloud user interface earlier).
     ```
     runmqakm -cert -add -db key.kdb -file qmgrcert_yyyymm.pem -label qmgrcert -stashed -type pkcs12 -format ascii
     ```
    1.3 Check your certificates have been added.
     ```
     runmqakm -cert -list -db key.kdb
     ```

     **Note:** The type parameter above is **pkcs12**.  Some samples suggest using **kdb**, but the resulting key.kdb is not readable by keytool, so for this exercise **pkcs12** is preferred.


## Next steps
{: #mqoc_chl_ssl_next}

### Securing Administration

The next step is to configure the client end of the communication to trust the queue manager certificate. Choose the administration tool that you would like to use and follow the appropriate instructions below.

* [Configuring security for remote administration using IBM MQ Explorer](/docs/services/mqcloud?topic=mqcloud-mqoc_remote_ssl_exp_admin)  
* [Configuring security for remote administration using runmqsc CLI](/docs/services/mqcloud?topic=mqcloud-mqoc_remote_ssl_runmqsc_admin)  

### Securing Application Connections

The next step is to configure your application connection so that it is uses TLS encryption when connecting to the queue manager.
* [Connect securely from MQI C & JMS application](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_ssl)
