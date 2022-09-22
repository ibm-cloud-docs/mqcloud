---
copyright:
  years: "2022"
lastupdated: "2022-07-25"

subcollection: mqcloud

keywords: secure, client, SSL, TLS, queue, manager, administration
---

{{site.data.keyword.attribute-definition-list}}

# Copying configuration from one queue manager to another
{: #mqoc_admin_qmcfgcp}

This document covers how to use the `dmpmqcfg` tool to store the configuration of a queue manager in an `mqsc` file, along with using `runmqsc` to apply this saved configuration to a different queue manager.

## Prerequisites
{: #mqoc_admin_qmcfgcp_prereq}

1. A secure connection to two existing queue managers (for instructions, follow the [creating a queue manager](/docs/services/mqcloud?topic=mqcloud-mqoc_create_qm) guide).
2. You have permission to access queue managers within your IBM MQ service instance (for instructions, follow the [configuring administrator access for a queue manager](/docs/services/mqcloud?topic=mqcloud-tutorial-configure-admin-access) guide).
    
  The user performing the following operations should be configured as an administrator of the queue manager as described [here](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-tutorial-configure-admin-access)
  {: important}

3. An existing installation of IBM MQ Client on your own machine.
 * Download the client from [here](https://www.ibm.com/support/pages/downloading-ibm-mq-930).{: external}
   * Clicking the **HTTP** link next to the latest available version of the **CD Clients** will take you to **Fix Central**. From there you can search for and select the appropriate **Redist** (redistributable) client bundle for your operating system platform. This will include the sample applications and `runmqsc`.
   * Once downloaded, unpack the bundle into a location of your choosing.
   * Make a note of the full path to the `bin` directory, the location of which will depend upon where you chose to unpack the bundle. This path will be referenced as `<PATH_TO_BIN_DIR>` for the rest of this task.
   * Make a note of the full path to the directory containing the sample applications. This path will be referenced as `<PATH_TO_SAMPLE_BIN_DIR>` for the rest of this task.
     * For Windows, this will be the `bin` directory unpacked in the previous step, the location of which will depend upon where you chose to unpack the bundle.
     * For Linux, this will be the `samp/bin` directory unpacked in the previous step, the location of which will depend upon where you chose to unpack the bundle.
 
  Mac users will need to also download the macos toolkit, which can be found [here](https://www14.software.ibm.com/cgi-bin/weblap/lap.pl?popup=Y&li_formnum=L-APIG-CAUEQC&accepted_url=https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/messaging/mqdev/mactoolkit/9.3.0.0-IBM-MQ-DevToolkit-MacX64.pkg){: external}
  {: important}

4. Follow the steps to [gather credentials and certificates for your queue managers](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#using-the-mq-on-cloud-service-console-to-gather-credentials-and-certificates) and [create a keystore in a PKCS12 format](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_configure_chl_ssl#mqoc_chl_ssl_keystore)

## Connecting to your remote queue managers 

To connect to your remote queue managers, a few environment variables must first be set.
We want to make sure that the `MQSERVER` value is empty. This can be achieved with the following:
`unset MQSERVER`

Assign the connection details and certificate gathered previously to `MQCCDTURL` and `MQSSLKEYR`:
* Linux:

  ```bash
  export MQCCDTURL=/path/to/file/connection_info_ccdt.json
  export MQSSLKEYR=/path/to/file/key
  ```
  {: pre}

* Windows:

  ```bash
  set  MQCCDTURL=\path\to\file\connection_info_ccdt.json
  set MQSSLKEYR=\path\to\file\key
  ```
  {: pre}

With these variables set, you can use `runmqsc` to test that your setup is correct: 

```bash
runmqsc -c -u <username> -w 60 <queue_manager_name>
```
{: pre}

When prompted, enter your apikey to authenticate, and you will be in the `runmqsc` console.
Simply type `quit` to exit the `mqsc` terminal.


## dmpmqcfg to generate mqsc file
{: #mqoc_admin_qmcfgcp_generate_mqsc}

The `dmpmqcfg` tool allows a user to create a copy of a queue manager's configuration, and saves it to a file. This file has multiple uses, such as a backup to help rebuild a queue manager if the configuration and log data are lost due to hardware failure and the queue manager is unable to restart or to be recovered from the log.

A small selection of optional parameters will be needed when using the `dmpmqcfg` tool. Firstly, make sure that all attributes are copied, this can be assured with the `-a` field. Second, a client mode connection needs to be forced, which can be achieved with `-c`. Use standard output redirection to store the definitions into a file. For example:

```bash
  dmpmqcfg -c default -m <queue_manager_1_name> -u <username> -a > /mq/backups/<queue_manager_1_name>.mqsc
````
{: pre}

When executed, you will be prompted for the apikey that allows you to connect to these queue managers.
Once supplied, the configuration file will be created in the specified location. 

## Applying the generated file to a different queue manager
{: #mqoc_admin_qmcfgcp_apply_mqsc}

Before applying the configuration to a new queue manager, your apikey needs to be added to the first line of the newly created file. The start of your file should look similar to the following:
```
<IBMCloud-apikey>
********************************************
*******************************************************************************
* Script generated on 2022-07-22   at 14.23.16 
* Script generated by user '<user>' on host '<host>' 
* Queue manager name: <queue_manager_1_name> 
* Queue manager platform: UNIX 
* Queue manager command level: (930/922)
* Command issued: dmpmqcfg -c default -m <queue_manager_1_name> -u <username> -a
*******************************************************************************
```

This is an important step as when running the next command, some of the optional parameters used won't provide a chance to input an apikey, but will instead read the first line of the specified file.
{: note}

With the apikey added to the configuration file, it can now be applied to other queue managers.
Using `runmqsc`, the optional parameter `-f <filename>` the input can be processed from the `.mqsc` file created in the previous task. The optional parameter `-c` must be used to ensure a client connection. The queue manager this configuration is being applied to must also be provided, for example:

```bash
runmqsc -f /mq/backups/<queue_manager_1_name>.mqsc -c -u <username> <queue_manager_2_name>
```

This will read the file created in the previous step and process every command. Once completed successfully, the settings of the second queue manager will match the settings of the first queue manager.

## Conclusion
{: #conc_mqoc_admin_qmcfgcp}

You have successfully:
* Created a configuration backup of a queue manager
* Applied a backup of a queue manager's configuration to a new queue manager.
