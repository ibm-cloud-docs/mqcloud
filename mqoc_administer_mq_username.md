---
copyright:
  years: 2017, 2019
lastupdated: "2018-06-06"

subcollection: mqcloud

keywords: user, application, edit, admin
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Editing or removing the username for an existing user or application
{: #mqoc_administer_mq_username}


## Editing the MQ username for an existing user or application
{: #mqoc_edit_mq_username}

These instructions will **edit** the MQ username for an existing user or application.
  * **Warning:** the user or application will no longer be able to connect to queue managers with the original MQ username.

1. Log in to the IBM Cloud console to view the dashboard.
2. In the **Resource summary** panel click **Services**.
3. In the **Offering** filter box type `MQ`.
4. Locate and click on your IBM MQ service instance, found under the 'Services' heading.
5. Click the appropriate tab, either **User credentials** or **Application credentials**.
6. Click the **Actions** menu **...** for the entry in the list of User or Application permissions that is to be edited.

 ![Image showing the location of the action button](./images/mqoc_admin_access_action_button.png)

7. Click **Edit MQ username**.
8. Enter a new MQ username.
  * Note: the MQ username must have a maximum of 12 characters and be lower case a-z or 0-9.  It must also be unique within your IBM MQ service instance.
9. Click **Save**.

---

## Removing access for an existing user or application
{: #mqoc_remove_qm_access}

These instructions will **remove** access for either an existing user or application.
  * **Warning:** your user or application will no longer be able to connect to queue managers within your IBM MQ service instance.

1. Follow steps **1** to **6** in the [Editing the MQ username for an existing user or application](#mqoc_edit_mq_username) section above.
2. Click **Remove user** or **Remove application**".
