---
copyright:
  years: 2017, 2019
lastupdated: "2018-02-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Users and Applications
{: #mqoc_users_and_applications}

**MQ on IBM Cloud** access control is managed by **IBM Identity And Access Management (IAM)**.
Permissions in the **IBM Cloud** are mapped to access rights in the **IBM MQ** queue managers within your IBM MQ service instance. The following describes how that mapping is achieved.

**MQ on IBM Cloud** makes a distinction between **Users** and **Applications** - which in **IAM** terminology are equivalent to  **Users** and **Service IDs**.
Both these entities are capable of accessing an **IBM MQ** queue manager but
they are in different groups and have different access rights.

Users are given an **IAM** access policy which automatically adds them to the standard  **mqm** group
for all queue managers in their service instance, and therefore they have full administrator access rights.

Applications are given an **IAM** access policy which automatically adds them to the
**mqwriters** group - this group gives applications permission to read/write to queues in the queue manager, but does
not give them administration privileges.

On deployment of a queue manager within **MQ on IBM Cloud**, two channels are created for you.
CLOUD_ADMIN_SVRCONN is a channel for administration, and is therefore accessible by **Users**.
CLOUD_APP_SVRCONN is a channel for queue access, and it therefore available to **Applications**.

## MQ Usernames

To access a queue manager using **IBM MQ** - a username and a password are required. The username is
restricted to 12 characters and must only contain lowercase (a-z) and numbers (0-9).

When creating users and applications in **MQ on IBM Cloud**, you are required to give these entities
a name (for a user, this must be a valid email address) from which a shorter name called **MQ username** is generated. This shorter user name is based on the longer name, but is guaranteed to be unique
within the service instance, and also conform to the required format of an **IBM MQ** username.

## Passwords

At the **MQ on Cloud** level, access control is implemented using **API keys**. These are used by our system as the passwords associated with users and applications at the **IBM MQ** level.

In the panel showing the list of queue managers in your service instance, you will find two tabs which
allow you to create **user permissions** and **application permissions**.

![alt text][screen1]

[screen1]: ./images/users.png "The tabs"

Users must generate and use their own platform API key - and this must be used as their password to connect to a queue manager.

The **Application permissions** panel allows you to create an individual API key associated with a specific
application. This is the password to be used with that application when connecting to
all queue managers in your service instance - thus each application has a different password.

---
