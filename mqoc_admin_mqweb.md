---
copyright:
  years: 2017, 2021
lastupdated: "2021-09-28"

subcollection: mqcloud

keywords: MQ, console, interface, admin, administration
---

{{site.data.keyword.attribute-definition-list}}

# Administering a queue manager using IBM MQ Console
{: #mqoc_admin_mqweb}

The MQ Web Console is an administration tool for IBM MQ that you access using a web browser running on your own machine. With the MQ Web Console, you can create a new queue, put a message onto the queue, browse the queue to view the message, and delete the queue.
{: shortdesc}

## Before you begin
{: #prereq_mqoc_admin_mqweb}

* An existing queue manager (for instructions, follow the [creating a queue manager](/docs/services/mqcloud?topic=mqcloud-mqoc_create_qm) guide).
* You have permission to access queue managers within your IBM MQ service instance (for instructions, follow the [configuring administrator access for a queue manager](/docs/services/mqcloud?topic=mqcloud-tutorial-configure-admin-access) guide).

## Login to the IBM Web Console for your queue manager
{: #connect_mqoc_admin_mqweb}

1. Log in to the IBM Cloud console.
2. Find your existing Service Instance, by entering part of its name in the search box and selecting your Service Instance, or:
    * Click the 'Hamburger menu'
    * Click 'Resource List'
    * Expand 'Services'
    * Click on your Service Instance
3. From the list of your queue managers, click on the queue manager you wish to administer.
4. Click the **Administration** tab.

    ![Image showing the Administration tab](./images/mqoc_administration_tab.png)

5. Click **Launch MQ Console**, this will open the 'IBM MQ Web Console' in a new browser tab.
    
    The **Launch MQ Console** button will only be available when the queue manager is running.
    {: note}

6. Click on Manage in the side menu to view your MQ objects

    ![Image showing the Web Console Manage tab](./images/mqoc_webconsole_managetab.png)

## Create a new test queue.
{: #createq_mqoc_admin_mqweb}

1. Ensure the 'Queues' tab is selected

    ![Image showing the + on the queues widgit](./images/mqoc_webconsole_queue_tab.png)

2. Click the **'Create +'** button.

    ![Image showing the + on the queues widgit](./images/mqoc_webconsole_create_queue.png)

3. Select a queue type of 'Local'.

4. Type in 'DEV.TEST.1'.

    The name can contain up to 48 characters. Valid characters are letters, numbers and the period, forward slash, underscore and percent symbols. The queue name needs to be unique within the queue manager.
    {: important}

5. Click **Create**.

You will see a success message, and your new queue now appears in the list.

## Put a message onto the test queue
{: #put_mqoc_admin_mqweb}

1. Click queue 'DEV.TEST.1'.

2. Click the **'Create +'** button.

3. Under 'Application data' enter a message

4. Click **Create**.

![Image showing the creation of a message on the queue](./images/mqoc_webcli_put.png)

You can see the message is now on the queue.

## Browse a message on the test queue
{: #get_mqoc_admin_mqweb}

1. Click on the message in the table.

You can see the details of the message. Expand 'Application data' to view the message text.

## Delete the test queue
{: #deleteq_mqoc_admin_mqweb}

1. Ensure the 'Queues' tab is selected

    ![Image showing the + on the queues widgit](./images/mqoc_webconsole_queue_tab.png)

2. Click on queue 'DEV.TEST.1'.

3. Click on the 3 dots button, then on 'Clear messages'

    ![Image showing the trash symbol on the queues widgit](./images/mqoc_webconsole_clear_messages.png)

4. Click on the 3 dots button, then on 'Configuration'

    ![Image showing the trash symbol on the queues widgit](./images/mqoc_webcli_queue_config.png)

5. Click **Delete Queue**.

    ![Image showing the trash symbol on the queues widgit](./images/mqoc_webcli_queue_delete.png)

You are returned to the 'Queues' tab. You can see that the test queue has been removed from the list of queues.

## Conclusion
{: #conc_mqoc_admin_mqweb}

You've successfully:

* Connected to a queue manager using the IBM MQ Web Console and have created a new test queue
* Put a test message onto the test queue and have browsed the test message
* Cleared and deleted the test queue to clean up

## Next steps
{: #next_mqoc_admin_mqweb}

Please see [Administration using the IBM MQ Console](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.adm.doc/q127570_.htm) for more information on what you can do with IBM Web Console.

[Connecting an application to a queue manager](/docs/services/mqcloud?topic=mqcloud-mqoc_connect_app_qm)

[Assigning user/group access to a queue](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_auth_record)
