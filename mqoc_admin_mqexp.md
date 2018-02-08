---
copyright:
  years: 2017, 2018
lastupdated: "2018-02-06"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administering a queue manager using MQ Explorer
{: #mqoc_admin_mqexp}

There are many actions you can perform through the MQ Explorer. You can:
* Connect to a queue manager
* Create a new queue
* Put a message onto a queue
* Browse a queue to view messages
* Delete a queue
{:shortdesc}

---

## Prerequisites
{: #prereq_mqoc_admin_mqexp}

* An existing queue manager (for instructions, follow the [creating a queue manager](mqoc_create_qm.html) guide).
* You have been granted permissions to access queue managers within your IBM MQ service instance. You have obtained your MQ username and have created your platform API key (for instructions, follow the [configuring administrator access for a queue manager](tutorials/tut_mqoc_configure_admin_qm_access.html) guide).
* An existing installation of IBM MQ Explorer (download and installation instructions can be obtained from [here](http://www-01.ibm.com/support/docview.wss?uid=swg24021041)).

---

## Gather required queue manager details
{: #getdetails_mqoc_admin_mqexp}

1. Log in to the IBM Cloud console.
2. Click on the 'hamburger menu'.
3. Click **Dashboard**.
4. Locate and click on your IBM MQ service instance, found under the 'Services' heading.
  * Ensure that **RESOURCE GROUP** is set to **All Resources** and **REGION** is set to **US South Region**.
5. From the list of your queue managers, click on the one you want to administer.
6. Make note of the **Queue manager name**, **Hostname** and **Port** values for use in the next steps.

---

## Connect to your queue manager using IBM MQ Explorer
{: #connect_mqoc_admin_mqexp}

1. Start IBM MQ Explorer.
2. In the 'MQ Explorer - Navigator' panel, expand **IBM MQ**.
3. Right click **Queue Managers**.
4. Click **Add Remote Queue Manager...**.
5. Input the queue manager name you want to administer.
6. Click **Next**.
7. Input the Hostname you noted in step 2.
8. Overwrite the Port number with the one you noted in step 2.
9. Overwrite the server connection channel name with **CLOUD.ADMIN.SVRCONN**.
10. Click **Next**.
11. Click **Next**.
12. Tick the checkbox for 'Enable user identification'.
13. Untick the checkbox for 'User identification compatibility mode'.
14. Type your **MQ username** as the user id.
15. Click **Finish**.
16. Paste your **platform API key** into the 'Password' text box.
17. Click **OK**.

Your queue manager connection now appears under the **Queue Managers** folder in the 'MQ Explorer - Navigator' panel.

---

## Create a new test queue called 'DEV.TEST.1'
{: #createq_mqoc_admin_mqexp}

In the 'MQ Explorer - Navigator > IBM MQ > Queue Managers' view:

1. Expand the entry for your queue manager.
2. Right click **Queues**.
3. Select 'New' > 'Local Queue...'.
4. Type 'DEV.TEST.1' in the 'Name' text box.
5. Click **Finish**.
6. Click **OK**.

Your new queue appears in the list of queues.

---

## Put a message onto the test queue
{: #put_mqoc_admin_mqexp}

1. Right click on queue 'DEV.TEST.1'.
2. Click 'Put Test Message...'.
3. Type in a test message in the 'Message data' text box.
4. Click **Put message**.
5. Click **Close**.
6. Click **Refresh** in the 'Queues' panel.

You can see that the 'Current queue depth' for 'DEV.TEST.1' is now **1**.

---

## Browse a message on the test queue
{: #get_mqoc_admin_mqexp}

1. Right click on queue 'DEV.TEST.1'.
2. Click 'Browse Messages...'.
3. Confirm you can see your test message and then click **Close**.

---

## Delete the test queue
{: #deleteq_mqoc_admin_mqexp}

1. Right click on queue 'DEV.TEST.1'.
2. Click 'Delete'.
3. Click 'Delete'.
3. Check the 'Clear all messages from the queue' box.
4. Click **Delete**.
5. Click **OK**.

You can see that queue 'DEV.TEST.1' has been removed from the list of queues.

---

## Conclusion
{: #conc_mqoc_admin_mqexp}

You've successfully:
* Connected to a queue manager using MQ Explorer and have created a new test queue
* Put a test message onto the test queue and have browsed the test queue to view the test message
* Cleared and deleted the test queue to clean up

---

## Next step
{: #next_mqoc_admin_mqexp}
[Connecting an application to a queue manager](/docs/services/mqcloud/mqoc_connect_app_qm.html)
