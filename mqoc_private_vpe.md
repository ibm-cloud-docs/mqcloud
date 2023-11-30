---
copyright:
  years: 2023
lastupdated: "2023-11-08"

subcollection: mqcloud

keywords: virtual private endpoint gateway
---

{{site.data.keyword.attribute-definition-list}}

# Virtual Private Endpoints (VPE)
{: #mqoc_private_vpe}

This guide walks you through accessing {{site.data.keyword.mq_full}} using Virtual Private Endpoints.
{: shortdesc}

When using Virtual Private Cloud (VPC) you can access both the {{site.data.keyword.mq_full}} deployment APIs and queue managers over the private IBM network by configuring Virtual Private Endpoint Gateways.

Using private endpoints requires the Server Name Indication (SNI) header to contain the hostname of the queue manager.  Therefore IBM MQ's multiple certificates capability is not supported in this environment.
{: attention}

## How to access the deployment API
{: #mqoc_private_vpe_api}

These steps will describe how to create a private connection between a VPC and the {{site.data.keyword.mq_full}} deployment APIs.

These instructions require that you already have created a {{site.data.keyword.mq_full}} **Reserved Deployment** service instance, deployed a queue manager and configured a VPC running the MQ Client.
{: requirement}

1. Create a virtual private endpoint gateway for the MQ VPE endpoint ending in **mq2.cloud.ibm.com** following [these steps](#mqoc_private_vpe_instructions)
1. Obtain an IAM access token using the API Key from the **User Credential** in the {{site.data.keyword.mq_full}} service instance using the [documented API](https://cloud.ibm.com/apidocs/iam-identity-token-api#gettoken-apikey)
1. Obtain the GUID of the MQ service instance from the IBM Cloud resource list view or using the [documented API](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#list-resource-instances)
1. Call the {{site.data.keyword.mq_full}} deployment API

    ```sh
    # ACCESS_TOKEN - IAM access token for the MQ user credential
    # REGION - Select to required region from running "ibmcloud regions"
    # GUID - The GUID of the service instance

    curl -X GET -H "Authorization: Bearer ${ACCESS_TOKEN}" "https://api.private.${REGION}.mq2.cloud.ibm.com/v1/${GUID}/options"
    ```
    {: codeblock}

For more details on the {{site.data.keyword.mq_full}} deployment APIs see [API documentation](https://cloud.ibm.com/apidocs/mq-on-cloud)

## How to access the queue manager
{: #mqoc_private_vpe_qm}

These instructions require that you already have created a {{site.data.keyword.mq_full}} **Reserved Deployment** service instance, deployed a queue manager and configured a VPC running the MQ Client.
{: requirement}

1. Create a virtual private endpoint gateway for the MQ VPE endpoint ending in **mq2.appdomain.cloud** following [these steps](#mqoc_private_vpe_instructions)
1. Configure access for the MQ client as described [here](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_configure_app_qm_access)
1. Configure the MQ Client ini file
    
    ```sh
    echo -e "SSL:\n  AllowTLSV13=TRUE\n  OutboundSNI=HOSTNAME" > ${HOME}/mqclient.ini
    export MQCLNTCF=${HOME}/mqclient.ini
    ```
    {: codeblock}

1. Configure and test the MQ client as described [here](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_connect_app_qm)
1. To administer the queue manager see available options [here](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_admin_qm)


## How to create a Virtual Private Endpoint Gateway (VPEG)
{: #mqoc_private_vpe_instructions}

The steps below describe how to create the virtual private endpoint gateway using the UI.  For more details on using the CLI or API see this [documentation](https://cloud.ibm.com/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=api)

1. Access the [IBM Cloud Console](https://cloud.ibm.com)
1. In the left side Navigation Menu select **VPC Infrastructure > Virtual private endpoint gateways**
1. Click the **Create** button
1. Under **Location**
    1. Select the **Geography** and **Region** that matches your {{site.data.keyword.mq_full}} instance
1. under **Details**
    1. Enter a **Name**
    1. Select a **Resource Group** or create a new one
    1. Optionally add tags
    1. Optionally add access management tags
    1. Select your Virtual Private Cloud (VPC) from the drop down
1. Under **Security groups**
    1. Select the Security Group you wish to use for controlling inbound and outbound traffic
    1. Update you security group rules to allow TCP traffic on port 443
        1. Click on the security group
        1. Click on the **Rules** tab
        1. Under **Inbound rules** click the **Create** button
        1. Select the Protocol **TCP**
        1. Select **Port Range** and specify a min of `443` and max of `443`
        1. Leave the **Source Type** as **Any**
        1. Click **Create**
1. Under **Request connection to service**
    1. For **Cloud service offerings** select **MQ**
    1. Select the **Cloud service region** that matches your {{site.data.keyword.mq_full}} instance
    1. Select the MQ VPE endpoint thats required
1. Under **Reserved IP**
    1. For **VPC endpoints** select **Select one for me**
    1. Enter a **Name** for the IP
    1. Select a **Subnet**
1. Click **Create virtual private endpoint gateway**
1. To ensure multi zone support an IP is required for each subnet in the VPC
    1. In the list of virtual private endpoint gateways click the one you just created
    1. Click the **Attached Resources** tab
    1. For each subnet Under **Reserved IPs**
        1. Click the **Reserve or bind IP** button
        1. For **VPC endpoints** select **Select one for me**
        1. Name the IP
        1. Select the subnet from the drop down
        1. Click **Reserve IP address**
