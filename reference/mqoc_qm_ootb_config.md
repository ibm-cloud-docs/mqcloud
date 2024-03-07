---
copyright:
  years: 2024
lastupdated: "2024-02-28"
keywords: IBM MQ, MQ on Cloud, MQ, Config, Configuration, Default, Objects
---

{{site.data.keyword.attribute-definition-list}}

# Out of the box Configuration
{: #out_of_the_box_configuration}

{{site.data.keyword.mq_full}} Queue Managers are created with a default configuration and a number of accompanying artifacts. 
{: shortdesc}

## Configuration
{: #configuration}

The following table shows the default {{site.data.keyword.mq_full}} Queue Manager configurations.

| Property | Value |
| --- | --- |
| `CHCKCLNT` | `REQUIRED` | 
| `CHCKLOCL` | `OPTIONAL` | 
| `ADOPTCTX` | `YES` |

## Queues
{: #queues}

The following list shows the default {{site.data.keyword.mq_full}} Queue Manager Queues.

- `DEV.QUEUE.1`
- `DEV.QUEUE.2`
- `DEV.QUEUE.3`
- `DEV.DEAD.LETTER.QUEUE`

## Topics
{: #topics}

The following list shows the default {{site.data.keyword.mq_full}} Queue Manager Topics.

- `DEV.BASE.TOPIC`

## Channels
{: #channels}

The following list shows the default {{site.data.keyword.mq_full}} Queue Manager Channels.

- `'CLOUD.ADMIN.SVRCONN'`
- `'CLOUD.APP.SVRCONN'`

The following table shows the default configurations for the listed channels.

| Property | Value |
| --- | --- |
| `CHLTYPE` | `SVRCONN` |
| `SSLCAUTH` | `OPTIONAL` |
| `SSLCIPH` | `ANY_TLS12_OR_HIGHER` |
