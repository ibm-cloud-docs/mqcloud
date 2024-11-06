---
copyright:
  years: 2017, 2021
lastupdated: "2021-09-28"

subcollection: mqcloud

keywords: admin, administration, runmqsc, SSL, TLS
---

{{site.data.keyword.attribute-definition-list}}

# Securing remote administration using runmqsc
{: #mqoc_remote_ssl_runmqsc_admin}

This document describes the process of enabling TLS for remote administration of an {{site.data.keyword.mq_short}} queue manager using the `runmqsc` command line interface.
{: shortdesc}

## Before you begin
{: #mqoc_remote_ssl_runmqsc_admin_prereq}

1. If your queue manager is version 9.2.1 revision 1 or older, you must first configure TLS security on the MQ channel. For newer versions, TLS is enabled by default with the ANY_TLS12_OR_HIGHER cipher. 
    - For details on how to enable TLS please refer to [Enabling TLS security for MQ channels in {{site.data.keyword.mq_short}}](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl).  
    - For the purposes of this topic we assume that the CLOUD.ADMIN.SVRCONN channel has been configured with the cipherspec ANY_TLS12_OR_HIGHER, and SSL Authentication (SSLCAUTH) as Optional
    - An additional section at the end of this topic describes how to extend the TLS configuration to support mutual TLS authentication of the runmqsc client
2. This topic describes using a JSON format CCDT to tell runmqsc how to connect to the queue manager
    - To use JSON format CCDT you must have a runmqsc installation from IBM MQ v9.1.2 or above. Runmqsc versions prior to this do not support JSON format CCDT
    - You can also connect runmqsc to a queue manager using a binary CCDT if you wish, but the instructions provided here are specific to JSON CCDT
3. To configure the client keystore file you will need tools such as `runmqakm`
    - These tools are available in either a full installation of IBM MQ, or an installation of the MQ client for your operating system
    - Both full and client installations are available from the [MQ Downloads](https://ibm.biz/MQdownloads){: external} page
    - There is also a [MacOS toolkit for Developers](https://developer.ibm.com/components/ibm-mq/tutorials/mq-macos-dev/){: external} client that allows native use of runmqsc on MacOS


## Configuring runmqsc to use standard ("one way") TLS connections
{: #mqoc_remote_ssl_runmqsc_admin_tasks}

### Download or create a JSON CCDT file that describes the queue manager you want to connect to

You can download a JSON CCDT from the queue manager details page by clicking on the "Connection information" button and then selecting the "JSON CCDT" format. Note that the downloaded JSON CCDT does not contain the cipher specification that you associated with the channel, so you have to include that manually by adding a transmissionSecurity definition for each channel as shown in the example below.

Alternatively you can simply copy the example template provided here and update the host, port, queueManager and channel values to match your queue manager.

```json
{
  "channel": [
  {
    "name": "CLOUD.ADMIN.SVRCONN",
    "clientConnection": {
      "connection": [
      {
      "host": "qm1-1234.qm.us-south.mq.appdomain.cloud",
      "port": 31500
      }
      ],
      "queueManager": "QM1"
    },
    "transmissionSecurity": {
      "cipherSpecification": "ANY_TLS12_OR_HIGHER"
    },
    "type": "clientConnection"
  }
  ]
}
```

The cipher specification in the JSON CCDT example above has been specified as ANY_TLS12_OR_HIGHER, which allows the runmqsc client to negotiate a permitted cipher with the queue manager within the family of TLS v1.2 ciphers, based on what ciphers the channel is configured to permit. For maximum flexibility the queue manager channel can also be configured as ANY_TLS12_OR_HIGHER which allows the client and server to negotiate between them.
{: note}

### Configure the necessary environment variables for the runmqsc environment

We will configure environment variables to instruct the runmqsc client to use the JSON CCDT to obtain the queue manager connection details, which includes the name of the channel cipher spec that we defined in the previous step.

1. Open a command prompt window and navigate to the MQ `bin` directory of your installation. The location of this will depend on your operating system, for example;
    | Operating System                          | file location                                    |
    | ----------------                          | -------------                                    |
    | Linux full MQ installation                | `/var/mqm/bin`                                   |
    | Windows                                   | `C:\Program Files\IBM\MQ\bin`                    |
    | Linux/Mac, using the client installation  | `~/mytoolkit/IBM-MQ-Toolkit-Mac-x64-9.1.2.0/bin` |
    {: caption="Installation file location for different Operating Systems" caption-side="bottom"}

2. Set the `MQCCDTURL` environment variable to instruct the runmqsc client to read the JSON CCDT, the `MQCCDTURL` variable is a URL pointing to the JSON CCDT file.
    - **MQCCCDTURL** is the full file path from the system root to the ccdt file.
        ```bash
        # Linux/MacOS
        export MQCCDTURL=file:///Users/myuser/connection_info_ccdt.json    
        unset MQSERVER

        # Windows
        set MQCCDTURL=file:///c:/temp/connection_info_ccdt.json    
        set MQSERVER=        
        ```
        {: codeblock}

        You *MUST NOT* have the MQSERVER variable set, otherwise that will take precedence over the settings from the JSON CCDT
        {: important}

    - There are two different ways of specifying your CCDT file location - if MQCCDTURL does not work for you, try setting MQCHLTAB and MQCHLLIB as described below.

      **MQCHLLIB** is the full path from the system root to the directory which holds the ccdt file.

      ```bash
      export MQCHLLIB=/path/to/ccdt
      set MQCHLLIB=c:\path\to\ccdt
      ```
      {: codeblock}

      **MQCHLTAB** is the filename of the ccdt file.

      ```bash
      export MQCHLTAB=connection_info_ccdt.json
      set MQCHLTAB=connection_info_ccdt.json
      ```    

3. Set the MQSSLKEYR environment variable to allow the runmqsc client to trust the TLS certificate presented by the queue manager

    The MQSSLKEYR variable must be set to the full path from the system root to a keystore file that contains the TLS certificate presented by the queue manager.

    If you do not have already have a keystore file then you can create one by following the [Create a keystore](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#mqoc_chl_ssl_keystore) topic, which includes downloading the public certificate for the queue manager from the service console user interface.

    Note that the `.kdb` suffix of the file must NOT be included in the `MQSSLKEYR` value - so for a key store named `key.kdb`, specify just `key`.  

    ```bash
    # Linux/MacOS
    export MQSSLKEYR=/Users/myuser/key

    # Windows
    set MQSSLKEYR=c:\temp\key
    ```
    {: codeblock}

### Execute the `runmqsc` command to connect to the queue manager

Now that we have set up the necessary environment we can execute the `runmqsc` command to connect to the queue manager.

As normal, you will need the following inputs to the runmqsc command:
- MQ Administrator username and API key, which you obtain from the service console as described in [Gather required connection details](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_mqcliexp#getdetails_mqoc_admin_mqcliexp). Note that this must an Administrator username and API key, and not an Application username and API key
- Queue manager name, which must match what is specified in the JSON CCDT file - for example "QM1"
```bash
<Path to MQ/bin directory>/runmqsc -c -u mqusername QM1
```

All the operations on this runmqsc will now run on a secured channel.

## Configuring runmqsc to use mutual ("two way") TLS connections
The following steps describe how to extend the instructions above to configure mutual TLS connectivity between the runmqsc client and the queue manager.

In mutual TLS scenarios the client (e.g. runmqsc) presents a client certificate to the queue manager, and the queue manager must be configured to trust that incoming client certificate.

1. Generate a TLS client certificate that will identify the runmqsc client:

    In some organizations TLS client certificates are generated for you by a central certificate authority (CA). For the purposes of this example we will generate our own self-signed client certificate.

    ```bash
    # Generate a new private key and public certificate for the client
    # (fill in the segments of the certificate as you wish when prompted)
    openssl req -newkey rsa:2048 -nodes -keyout clientKey.pem -x509 -days 365 -out clientCert.pem

    # Combine the private key and public certificate into a single file
    cat clientKey.pem > clientCombined.pem
    cat clientCert.pem >> clientCombined.pem
    ```
    {: codeblock}

2. Add the newly generated client certificate to the local keystore file:

    Import the combined client key/cert into the keystore file, making a note of the label that you use.
    ```bash
    runmqakm -cert -add -db key.kdb -file clientCombined.pem -label runmqsc -stashed -type pkcs12 -format ascii
    ```
    {: pre}

3. Configure the queue manager to trust the client certificate:
    - Import the public part of the client certificate by navigating to the queue manager details page in the {{site.data.keyword.mq_short}} service console user interface, and selecting the "Trust store" tab
    - Click the "Import certificate" button, and select the file containing the public part of the client certificate, for example `clientCert.pem`
    - Click Next and pick a label for the certificate (it doesn't have to be the same label as in the client keystore file), then click Save
    - Once the certificate has been uploaded you will be requested to refresh the queue manager SSL security configuration which you can do using MQ Console, MQ Explorer or runmqsc as [described here](/docs/services/mqcloud?topic=mqcloud-mqoc_refresh_security)

4. Configure the queue manager channel to require mutual TLS:
    - The TLS mode for a channel is controlled by the `SSL Authentication` attribute of the channel, which must be set to `Required` to enable mutual TLS. You can set the attribute using MQ Console or MQ Explorer via the UI, or if you are using runmqsc then you must set the attribute `SSLCAUTH` to `REQUIRED`.

5. Configure runmqsc to present the client certificate when it connects to the queue manager:
    - Set the `MQCERTLABL` environment variable to the label of the client certificate in the local keystore file, and then you can execute the runmqsc command to connect to the queue manager, which this time will be configured using mutual TLS authentication.

    ```bash
    export MQCERTLABL=runmqsc
    runmqsc -c -u mqusername QM1
    ```
    {: codeblock}

## Next steps
{: #mqoc_remote_ssl_runmqsc_admin_next}

If you want to connect applications to a queue manager that has TLS enabled on the channels then you can follow the instructions in the following topic;
* [Connect securely from C MQI & JMS application](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_ssl)
