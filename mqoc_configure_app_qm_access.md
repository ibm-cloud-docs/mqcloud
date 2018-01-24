---
copyright:
  years: 2017, 2018
lastupdated: "2018-01-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring access for connecting an application to a queue manager
{: #mqoc_configure_app_qm_access}

To connect an application to a queue manager, you need the necessary set of credentials: 
* An application must connect to a queue manager as either the **app1** or **app2** user name
* The password must be a valid **API Key** for a Service ID in your account that has the appropriate access for the **IBM MQ** service.
{:shortdesc}

 * User name **app1** has access to connect to all queues and topics starting with **DEV.***.  It has permission to **put / get** messages and **publish / subscribe** to topics.
 * User name **app2** has access to connect to all queues and topics starting with **DEV.***.  It has permission to **get** messages and **subscribe** to topics.

**Note:** This guide is for the **experimental** release of the **IBM MQ** service, so the process for authentication/authorization is currently limited.

---

The following steps must be completed by a user who has been granted **Administrator** access for the **IBM MQ** service or has the **Administrator** role for your **Account**.

## Part A. Creating a Service ID
{: #parta_mqoc_configure_app_qm_access}

1. From the top right menu bar, click **Manage > Security > Identity and Access**, and then click **Service IDs**.
2. Click **Create**.
3. Enter a **Name** and **Description** that will help you identify your application.
 * Note that the name must be unique for each Service ID you create for an application.
4. Click **Create**.

## Part B. Granting an application access to your queue managers
{: #partb_mqoc_configure_app_qm_access}

1. Click the **Service ID** that you created in Part A.
2. Click **Assign access**.
3. Click **Assign access to resources**.
4. Select service **IBM MQ**.
5. Select **All regions**.
6. Select **All service instances**.
7. If your application will connect as the **app1** user name, then select the **Editor** role.  If your application will connect as the **app2** user name, then select the **Viewer** role.
8. Click **Assign**.

## Part C. Creating an API Key
{: #partc_mqoc_configure_app_qm_access}

The API Key that is generated in these steps is used to authenticate your **application** with **IBM Cloud**. Therefore, it should be stored securely.

1. From the tab bar, click **API Keys**.
2. Click **Create**.
3. Enter a **Name** and **Description** that will help you identify your application API Key.
4. Click **Create**.
5. Click **Show** to display the API key to copy and save it for later, or click **Download** to store the API Key in a file.

 **Note:** For security reasons, the API key is only available to be copied or downloaded at the time of creation. If the API key is lost, you must create a new API key.

---

## Next step
{: #next_mqoc_configure_app_qm_access}

[Connecting an application to a queue manager](/docs/services/mqcloud/mqoc_connect_app_qm.html)
