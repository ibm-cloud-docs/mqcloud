---
copyright:
  years: 2017
lastupdated: "2017-12-6"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring administrator access for a queue manager
{: #tut_mqoc_configure_admin_qm_access}

You need to get the necessary user credentials to administer your queue managers. The administration of a queue manager (using IBM MQ Web Console, IBM MQ Explorer or runmqsc) must be done using **admin** as the user name.  The password must be a valid **API Key** for a user in your account who has **Administrator** access for the **IBM MQ** service.
{:shortdesc}

**Note:** This guide is for the **experimental** release of the **IBM MQ** service. Future releases of this service will have an enhanced process for authentication/authorization.

---

## Part A. Checking your current IBM MQ service access rights
{: #parta_tut_mqoc_configure_admin_qm_access}

To check your access rights:
1. From the top right menu bar, click **Manage > Security > Identity and Access**, and then click **Users**.
2. Click on your **User** to view your access rights.

If you have the **Administrator** role for your **Account** and/or you have the **Administrator** role for Policy **ALL 'IBM MQ' resources**, then you already have administrator access to the **IBM MQ** service. In this case, skip **Part B** and complete **Part C. Creating an API Key**.

Otherwise, please ask an administrator of your account to complete **Part B. Granting a user administrator access to the IBM MQ service**. Once they have completed this, re-check your access rights are correct before moving on to **Part C. Creating an API Key**.

## Part B. Granting a user administrator access to the IBM MQ service
{: #partb_tut_mqoc_configure_admin_qm_access}

These steps must be performed by a user who has access to manage users in your account.

1. From the top right menu bar, click **Manage > Security > Identity and Access**, and then click **Users**.
2. Click the **User** that you want to grant administrator access to the **IBM MQ** service.
3. Click **Assign access**.
4. Click **Assign access to resources**.
5. Select service **IBM MQ**.
6. Select **All regions**.
7. Select **All service instances**.
8. Select the **Administrator** role.
9. Click **Assign**.

## Part C. Creating an API Key
{: #partc_tut_mqoc_configure_admin_qm_access}

The API Key that is generated in these steps is used to authenticate with **IBM Cloud** as the **user** who created it.  Therefore, it should not be shared with any other users and should be stored securely.

1. From the top right menu bar, click **Manage > Security > Platform API Keys**.
2. Click **Create**.
3. Enter a **Name** and **Description** that will help you identify your user API Key.
4. Click **Create**.
5. Click **Show** to display the API key to copy and save it for later, or click **Download** to store the API Key in a file.

**Note:** For security reasons, the API key is only available to be copied or downloaded at the time of creation.  If the API key is lost, you must create a new API key.

---

## Next step
{: #next_tut_mqoc_configure_admin_qm_access}

Administer a queue manager, using one of the [queue manager administration options](/docs/services/mqcloud/mqoc_admin_qm.html)
