---
copyright:
  years: 2018, 2021
lastupdated: "2025-06-27"
---

{{site.data.keyword.attribute-definition-list}}

# Invoking the queue manager REST APIs
{: #mqoc_qm_rest_api}

IBM MQ provides a set of REST APIs that provide a simple way to administer, test and interact with your queue manager via scripts, applications and programs. In this section, the requirements to call the APIs on the IBM queue manager will be provided, in addition to examples that can be run straight from your terminal and be easily translated into other programming languages.

An IBM queue manager has 2 REST APIs available to call:
 * Administration REST API - that allows you carry out administrative actions against the queue manager
 * Messaging REST API - that allows applications to send and receive messages

There are a few important pieces of information when interacting with the IBM queue manager:
 1. The Listener Port is not required in the URI to call the REST API
 2. The hostname to call your queue manager should start with `web-`
 3. The beginning of the path in the URI should be `/ibmmq/rest`
 4. The REST API is case-sensitive - for example if your queue manager is called QM1 and your using the admin REST API, then in the path for admin you should do `/qmgr/QM1/..`.
{: shortdesc}

## Authenticating your client to invoke REST API requests
{: #mqoc_qm_restlogin}

There are a couple of ways that you can authenticate with your IBM queue manager over REST.

The method described below is token-based authentication, interacting with the Login REST API exposed by the queue manager. This REST API returns a cookie that can be saved to a variable in your script/application or in a plain text file that can be used by subsequent requests to your queue manager.

Once you have finished interacting with the IBM queue manager over REST, the Login REST API can also be used to revoke the access token, requiring the client to retrieve a new access token before making subsequent calls.

For more information on how to use token-based authentication to interact with your queue manager over REST see [here](https://www.ibm.com/docs/en/ibm-mq/9.4.x?topic=security-using-token-based-authentication-rest-api).

Your queue manager hostname will differ per queue manager and per region, but will look similar to `qm1-abcd.qm.eu-gb.appdomain.cloud`

### Example: Authenticating with an IBM queue manager using a session cookie

```bash
curl -X POST https://web-<queue_manager_hostname>/ibmmq/rest/v3/login -H "Content-Type: application/json" --data "{\"username\":\"<MQ_USERNAME>\",\"password\":\"<API_KEY>\"}" -c cookiejar.txt
```
{: pre}

In subsequent calls pass the `cookiejar.txt` file as a parameter to identify yourself as an authenticated user.
{: important}

For more ways and information on how you can authenticate with your IBM queue manager over REST, see [here](https://www.ibm.com/docs/en/ibm-mq/9.4.x?topic=mcras-configuring-client-certificate-authentication-rest-api-mq-console)

## Administering the queue manager
{: #mqoc_qm_restadmin}

The admin REST API enables the ability to administer the queue manager, allowing you to create, retrieve, modify and delete queues.

The admin REST API documentation can be found [here](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.1.0/com.ibm.mq.dev.doc/q130960_.htm).

### Example: Creating a queue in an IBM queue manager

If you have authenticated using token-based authentication, point to the place you stored your cookie to identify yourself as an authenticated user.

```bash
curl -X POST https://web-<queue_manager_hostname>/ibmmq/rest/v3/admin/action/qmgr/<queue_manager_name>/mqsc -H "Accept: application/json" -H "Content-Type: application/json" -H "ibm-mq-rest-csrf-token: value" --data '{
  "type": "runCommand",
  "parameters": {
    "command": "DEFINE QLOCAL(TEST.QUEUE)"
  }
}' -b cookiejar.txt
```
{: pre}

You can then display the created queue by running the following command.

```bash
curl -X POST https://web-<queue_manager_hostname>/ibmmq/rest/v3/admin/action/qmgr/<queue_manager_name>/mqsc -H "Accept: application/json" -H "Content-Type: application/json" -H "ibm-mq-rest-csrf-token: value" --data '{
  "type": "runCommand",
  "parameters": {
    "command": "DISPLAY QLOCAL(TEST.QUEUE)"
  }
}' -b cookiejar.txt
```
{: pre}

## Sending and receiving messages
{: #mqoc_qm_restmessaging}

The messaging REST API allows you to send and retrieve messages on a desired queue within an IBM queue manager.

The messaging REST API documentation can be found [here](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.1.0/com.ibm.mq.dev.doc/q130960_.htm){: external}.

### Non 'DEV.' queues

If a new queue has been created whose name does not start with 'DEV.' the predefined authorization records will not apply. Therefore applications will not have the required permissions to send or receive messages to this queue. Review the [Assigning user/group access to a queue](/docs/services/mqcloud?topic=mqcloud-mqoc_configure_auth_record) guide for more information and for the steps required to configure the authorization record required for this queue.

### Example: Putting a message on a queue in an IBM queue manager

If you have authenticated using token-based authentication, point to the place you stored your cookie to identify yourself as an authenticated user.

```bash
curl -X POST https://web-<queue_manager_hostname>/ibmmq/rest/v3/messaging/qmgr/<queue_manager_name>/queue/<queue_name>/message -H "Content-Type: text/plain" -H "ibm-mq-rest-csrf-token: value" --data "hello world" -b cookiejar.txt
```
{: pre}

Please note that by default any messages sent via the messaging REST API will be treated as non-persistent, regardless of the target queue's configured default persistence setting.
To change the default behaviour, you can include an optional header `ibm-mq-md-persistence` which must be specified as one of the following values:
    - *persistent*
    - *nonPersistent*

To send a persistent message, the example above would then take the following form:

```bash
curl -X POST https://web-<queue_manager_hostname>/ibmmq/rest/v3/messaging/qmgr/<queue_manager_name>/queue/<queue_name>/message -H "Content-Type: text/plain" -H "ibm-mq-rest-csrf-token: value" -H "ibm-mq-md-persistence: persistent" --data "hello world" -b cookiejar.txt
```
{: pre}

The full list of messaging REST API headers can be found [here](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.1.0/com.ibm.mq.ref.dev.doc/q130740_.htm){: external}
