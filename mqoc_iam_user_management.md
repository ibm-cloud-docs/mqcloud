---
copyright:
  years: 2025
lastupdated: "2025-18-08"

subcollection: mqcloud

keywords: iam, user, application, edit, admin
---

{{site.data.keyword.attribute-definition-list}}

# Configuring IAM Users for {{site.data.keyword.mq_full}}

This guide applies to managing users for the {{site.data.keyword.mq_short}} Reserved Deployment Service plan only and is only available in limited regions.
{: attention}

## Use Case

The following guide will allow an {{site.data.keyword.mq_short}} administrator to create and manage user permissions via the use of Service IDs and Access Groups rather than through {{site.data.keyword.mq_short}} directly. This allows for better separation of duties for the users of your {{site.data.keyword.mq_short}} service instance and gives a central location to manage users through IAM instead of through individual Queue Managers.
{: shortdesc}

This guide assumes you already have a running Queue Manager within your Reserved Deployment Instance and have the necessary IAM access to make a Service ID, Access Group and administer your Reserved Deployment Service instance.
{: requirement}

## Creating and Managing Users in IAM

You will require necessary permissions for creating and managing Service IDs and Access Groups. For more details on managing IAM users, see [here](https://cloud.ibm.com/docs/account?topic=account-iamuserinv&interface=ui)

1. Create a new [Service ID](https://cloud.ibm.com/iam/serviceids/ServiceId-6dc1a280-1de4-4831-b7aa-bbf1cfc5941f?tab=iam), or use an existing one
1. Create a new [Access Group](https://cloud.ibm.com/iam/groups)
   - Add the Service ID you created to the Access Group under the `Service IDs` tab
1. Under the `Access` tab of this new Access Group, assign a new access:
   - `Service` should be MQ
   - `Resources` should be scoped accordingly; available scopes include your Account, Region, Reserved Deployment Service or Resource Group. For example, scoping to a specific Reserved Deployment Service:
     - `Attribute`: Service Instance
     - `Operator`: string equals
     - `Value`: Your Service Instance CRN
   - `Roles and Actions` should be scoped based on your specific needs:
     - `Writer` grants **messaging-level access** (the ability to put and get messages to Queue Managers)
     - `Manager` grants **full admin access** to the {{site.data.keyword.mq_short}} Queue Managers (full administration access, ability to create Queues etc)
1. After creating this new Access Group, check the `IAM Managed Credentials` tab on the `Manage` page of your Reserved Deployment Instance. You should be able to see the Service ID you created.

## Get a List of Users with Short Names

To retrieve a list of users (including their short names) for a Service Instance, you can make a GET request to the Users API.

Prerequisites:

- You must have a valid [IAM Access Token](https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey). This is `<IAM_TOKEN>` in the command below
- You must set up authentication for the [{{site.data.keyword.mq_short}} APIs](https://cloud.ibm.com/apidocs/mq-on-cloud#authentication)
- You need the [Service Instance GUID](https://cloud.ibm.com/docs/key-protect?topic=key-protect-retrieve-instance-ID&interface=ui) for your Reserved Deployment instance. This is `<SERVICE_INSTANCE_GUID>` in the command below
- Determine the correct [base url](https://cloud.ibm.com/apidocs/mq-on-cloud#endpoint-url) for your Service Instance based on its region. This is `<BASE_URL>` in the command below

```bash
curl -X GET --location --header "Authorization: Bearer <IAM_TOKEN>" --header "Accept: application/json" "<BASE_URL>/v1/<SERVICE_INSTANCE_GUID>/users"
```
{: pre}

An example response for the above command is:

```json
{
  "offset": 0,
  "limit": 25,
  "first": {
    "href": "https://api.private.eu-de.mq2.cloud.ibm.com/v1/a2b4d4bc-dadb-4637-bcec-9b7d1e723af8/users?limit=25"
  },
  "users": [
    {
      "id": "8414515e99e16c988f",
      "name": "testuser",
      "email": "NOT APPLICABLE",
      "iam_service_id": "iam-ServiceId-6c213316-ca90-45g1-84c6-9bcf0e06a636",
      "href": "https://api.private.eu-de.mq2.cloud.ibm.com/v1/a2b4d4bc-dadb-4637-bcec-9b7d1e723af8/users/31a413dd84346effd8895b6ba4641641"
    }
  ]
}
```

## Update a User’s Short Name

After creating the Access Group, your Service ID will have been added to your Reserved Deployment Instance with an auto-generated shortname. You can update the shortname if required by sending a PATCH request to the Users API.

Prerequisites:

- You must have a valid [IAM Access Token](https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey). This is `IAM_TOKEN` in the command below
- You must set up authentication for the [{{site.data.keyword.mq_short}} APIs](https://cloud.ibm.com/apidocs/mq-on-cloud#authentication)
- You need the [Service Instance GUID](https://cloud.ibm.com/docs/key-protect?topic=key-protect-retrieve-instance-ID&interface=ui) for the relevant Reserved Deployment instance. This is `<SERVICE_INSTANCE_GUID>` in the command below
- Determine the correct [base url](https://cloud.ibm.com/apidocs/mq-on-cloud#endpoint-url) for your Service Instance. This is `<BASE_URL>` in the command below
- Determine the User ID for the user you want to update, this can be retrieved by the API call in the previous stage of these instuctions. This is `<USER_ID>` in the command below

The new short name must be:

- lowercase
- 1–12 characters
- match the regex: `^[a-z][-a-z0-9]\*$`
- unique across your Reserved Deployment instances

```bash
curl -X PATCH --location --header "Authorization: Bearer <IAM_TOKEN>" --header "Accept: application/json" --header "Content-Type: application/json" "<BASE_URL>/v1/<SERVICE_INSTANCE_GUID>/users/<USER_ID>"  --data '{ "shortname": "<NEW_SHORT_NAME>" }'
```
{: pre}

An example response for the above command is:

```json
{
  "id": "8414515e99e16c988f",
  "name": "updatedtestuser",
  "email": "NOT APPLICABLE",
  "iam_service_id": "iam-ServiceId-6c213316-ca90-45g1-84c6-9bcf0e06a636",
  "href": "https://api.private.eu-de.mq2.cloud.ibm.com/v1/a2b4d4bc-dadb-4637-bcec-9b6d1e723af8/users/31a413dd54346effc7895b6ba4641641"
}
```

## Updating a User's Short Name using the Terraform Module

You can also manage users using the {{site.data.keyword.mq_short}} Terraform Module. Instructions on how to set up the provider can be found [here](https://github.com/IBM-Cloud/terraform-provider-ibm?tab=readme-ov-file#download-the-provider-manually-option-2)

1. After setting up and authenticating the provider, create a `main.tf` file with an empty user block:

```terraform
resource "ibm_mqcloud_user" "user1" {

}
```
{: pre}

2. Import a user to your terraform instance using `terraform import`, retrieving the Service Instance GUID and User ID in the same way as for the API instructions above

```bash
terraform import  "ibm_mqcloud_user"."user1" ${service_instance_guid}/${user_id}
```
{: pre}

3. Update the terraform state file to include the imported users details as per details [here](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/mqcloud_user)

```terraform
resource "ibm_mqcloud_user" "user1" {
  name = "testuser"
  service_instance_guid = "8f3390a1-0de1-45e9-a3ad-31f1678244ac"
}
```
{: pre}

4. Update the value of `name` and run `terraform apply`
5. The name of the user will be updated

## Configuring Authority for each User/Certificate

Once you have a User configured in your Queue Manager using any of the methods above, you can create a certificate for each user or application you want to connect.

For example, the following `SSLPEER` maps a certificate with a common name of `application1` and an organisational unit (OU) of `team1` to user `user1`. In addition to the `SSLPEER`, you should also specify `SSLCERTI` to be very specific about the issuer of the certificate. The `MCAUSER` is the user name that you have created in IAM with {{site.data.keyword.mq_short}} access.

```bash
SET CHLAUTH('MTLS.SVRCONN') TYPE(SSLPEERMAP) SSLPEER('CN=application1,OU=team1') SSLCERTI('CN=applicationCA,OU=Certificate Authority') USERSRC(MAP) MCAUSER('user1') ACTION(REPLACE)
```
{: pre}

For more information on using custom certificates, see [here](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_qm_certs#own_cert_mqoc_qm_certs).
