---
copyright:
  years: 2017, 2022
lastupdated: "2022-10-21"

content-type: tutorial
account-plan: paid
completion-time: 20m
services:
---

{{site.data.keyword.attribute-definition-list}}

# Configuring administrator access for a queue manager
{: #tutorial-configure-admin-access}
{: toc-content-type="tutorial"}
{: toc-services=""}
{: toc-completion-time="20m"}

In this tutorial you learn how to configure administration access for a queue manager you have created.
{: shortdesc}

To administer a queue manager (using IBM MQ Web Console, IBM MQ Explorer or runmqsc) an administrator must be granted permissions to access queue managers within their IBM MQ service instance. They must connect to the queue manager using their **Administrator username** and the password must be their **Administrator API key**.

## Before you begin
{: #configure-admin-access-prereqs}

* [Create an MQ Service instance](/docs/mqcloud?topic=mqcloud-mqoc_create_qm)
* [Understand IBM MQ administrators and applications](/docs/mqcloud?topic=mqcloud-users_and_apps) 
* Ensure you have the following priviliges:
    * Administrator for the **MQ** service in the required Resource Group
    * Administrator for the **User Management** service in account management services
    * The account owner will need to set [unrestricted visibility of the user list in the account](/docs/account?topic=account-iam-user-setting#userlistview)


## Creating Administrator Credentials
{: #configure-admin-create-credentials}
{: step}

1. Log in to the IBM Cloud console to view the dashboard.
2. In the **Resource summary** panel click **Services**.
3. In the **Offering** filter box type `MQ`.
4. Locate and click on your IBM MQ service instance, found under the 'Services' heading.
5. Once in the MQ on Cloud service, click the **User credentials** tab.

    ![Image showing the location of the User credentials tab](../images/mqoc_admin_access_user_perms_tab.png)

6. Click **Add**.
7. Enter the user's **Email address**.
8. Click **Generate MQ username**.

    A unique administrator username will be auto-generated for the user.  You can edit the text-box to change this to the preferred username.  It must have a maximum of 12 characters and be lower case a-z or 0-9.  It must also be unique within your IBM MQ service instance.
    {: note}

9. Click **Add credentials**.

The user that was added will now have permissions to access queue managers within your IBM MQ service instance.  The user can view their **Administrator username** and obtain their **Administrator API key** by following the instructions for administering a queue manager (see **Next step**).

## Next steps
{: #configure-admin-next-steps}

Administer a queue manager, using one of the [queue manager administration options](/docs/services/mqcloud?topic=mqcloud-mqoc_admin_qm)
