---
copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Queue manager REST APIs
{: #mqoc_qm_rest_api}


IBM MQ provides a set of REST APIs that provide a simple way to administer, test and interact with your queue manager via scripts, applications and programs. In this section, the requirements to call the APIs on the IBM queue manager will be provided, in addition to examples that can be run straight from your terminal and be easily translated into other programming languages.

An IBM queue manager has 2 REST APIs available to call:
 * Administration REST API - that allows you carry out administrative actions against the queue manager
 * Messaging REST API - that allows applications to send and receive messages

NOTE: There are a few important pieces of information when interacting with the IBM queue manager:
 1. The Listener Port is not required in the URI to call the REST API
 2. The hostname to call your queue manager should start with `web-`
 3. The beginning of the path in the URI should be `/ibmmq/rest`
 4. The REST API is case-sensitive - for example if your queue manager is called QM1 and your using the admin REST API, then in the path for admin you should do `/qmgr/QM1/..`.
{:shortdesc}

---
## Authenticating your client to invoke REST API requests
{: #mqoc_qm_restlogin}

There are a couple of ways that you can authenticate with your IBM queue manager over REST.

The first is using Basic Authentication, this is very common method used to interact with the queue manager over REST as it is easy to convert to other languages and is great for testing.

For more information on using Basic Authentication to authenticate with your queue manager see [here](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.1.0/com.ibm.mq.sec.doc/q128710_.htm).

__Example: Authenticating with an IBM queue manager using Basic Authentication__

1. Get your MQ username and API key from your service instance in IBM Cloud, then run the following:  
```
AUTH=`echo "<MQ_USERNAME>:<API_KEY>" | base64`
```
NOTE: The `MQ_USERNAME` and `API_KEY` will depend on what REST API you are accessing:
 * admin, you need to add your user in the user permissions tab which will generate you a MQ username and use your platform API key for IBM Cloud
 * messaging, you need to create an application permission in the application permissions tab and use the API key and the MQ username it generates for you
2. Pass in the value of `AUTH` in the Authorization header of your requests:
```
curl -H "Authorization: Basic $AUTH" -H "ibm-mq-rest-csrf-token: value" https://web-qm1-abcd.qm.eu-gb.mqcloud.ibm.com/ibmmq/rest/v1/admin/qmgr/qm1
```

The second method is token-based authentication, interacting with the Login REST API exposed by the queue manager. This REST API returns a cookie that can be saved to a variable in your script/application or in a plain text file that can be used by subsequent requests to your queue manager.

Once you have finished interacting with the IBM queue manager over REST, the Login REST API can also be used to revoke the access token, requiring the client to retrieve a new access token before making subsequent calls.

For more information on how to use token-based authentication to interact with your queue manager over REST see [here](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.1.0/com.ibm.mq.sec.doc/q128720_.htm).

__Example: Authenticating with an IBM queue manager using a session cookie__
```
curl -X POST https://web-qm1-abcd.qm.eu-gb.mqcloud.ibm.com/ibmmq/rest/v1/login -H "Content-Type: application/json" --data "{\"username\":\"<MQ_USERNAME>\",\"password\":\"<API_KEY>\"}" -c cookiejar.txt
```
NOTE: In subsequent calls pass the `cookiejar.txt` file as a parameter to identify yourself as an authenticated user.

---
## Administering the queue manager
{: #mqoc_qm_restadmin}

The admin REST API enables the ability to administer the queue manager, allowing you to create, retrieve, modify and delete queues.

The admin REST API documentation can be found [here](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.1.0/com.ibm.mq.dev.doc/q130960_.htm).

__Example: Creating a queue in an IBM queue manager__

If you have authenticated using token-based authentication, point to the place you stored your cookie to identify yourself as an authenticated user.
```
curl -X POST https://web-qm1-abcd.qm.eu-gb.mqcloud.ibm.com/ibmmq/rest/v1/admin/qmgr/qm1/queue -H "Content-Type: application/json" -H "ibm-mq-rest-csrf-token: value" --data "{\"name\":\"TEST.QUEUE\"}" -b cookiejar.txt
```

---
## Sending and receiving messages
{: #mqoc_qm_restmessaging}

The messaging REST API allows you to send and retrieve messages on a desired queue within an IBM queue manager.

The messaging REST API documentation can be found [here](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.1.0/com.ibm.mq.dev.doc/q130960_.htm).

__Example: Putting a message on a queue in an IBM queue manager__

If you have authenticated using token-based authentication, point to the place you stored your cookie to identify yourself as an authenticated user.
```
curl -X POST https://web-qm1-abcd.qm.eu-gb.mqcloud.ibm.com/ibmmq/rest/v1/messaging/qmgr/qm1/queue/TEST.QUEUE/message -H "Content-Type: text/plain" -H "ibm-mq-rest-csrf-token: value" --data "hello world" -b cookiejar.txt
```
