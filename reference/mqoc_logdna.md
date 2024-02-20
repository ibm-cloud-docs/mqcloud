---

copyright:
  years: 2020, 2023
lastupdated: "2023-05-17"

keywords: IBM MQ, MQ on Cloud, MQ, LogDNA, Logs, Logging

---

{{site.data.keyword.attribute-definition-list}}

# LogDNA Logs
{: #logdna_logs}

{{site.data.keyword.mq_full}} generates platform services logs that are displayed in your LogDNA instances.
{: shortdesc}

For information about how to configure LogDNA instances to receive platform services logs, see [Configuring IBM Cloud service logs](/docs/log-analysis?topic=log-analysis-config_svc_logs).

{{site.data.keyword.mq_full}} generates platform services logs that are displayed in your LogDNA instances for the following specific cases:

- When the queue manager error logs are updated

## Where to look for {{site.data.keyword.la_full_notm}} logs
{: #registry_logs_region}

The [region](/docs/mqcloud?topic=mqcloud-deploy_locations) in which an MQ on Cloud log entry is available corresponds to the region of the queue manger that generated the log.

The following table shows the location of MQ on Cloud logs.

| Region for your MQ on Cloud instance | Location of {{site.data.keyword.la_full_notm}} logs |
|-----------------                     |-----------------                                    |
| `us-south`                           | `Dallas (us-south)`                                 |
| `us-east`                            | `Washington DC (us-east)`                           |
| `eu-de`                              | `Frankfurt (eu-de)`                                 |
| `eu-gb`                              | `London (eu-gb)`                                    |
{: caption="Table 1. Location of {{site.data.keyword.la_full_notm}} logs" caption-side="top"}

## MQ Queue Manager log analysis

### Key MQ log fields for debug

| Label                                | Explanation                                               |
|-----------------                     |-----------------                                          |
| `ibm_messageId`                      | Starting `AMQ` - this value refers to the category of the IBM MQ diagnostic message, see reference https://www.ibm.com/docs/en/ibm-mq/9.3?topic=codes-amq-messages-multiplatforms for further detail  |
| `ibm_version`                        | The MQ version in the form `9.3.4.0`                      |
| `loglevel`                           | The level of log, for example `WARNING` or `ERROR`        |
| `ibm_serverName`                     | The name of the QueueManager                              |
{: caption="Table 1. Key MQ log fields for debug" caption-side="top"}

For a full reference on all of the available fields for MQ log messages, see https://www.ibm.com/docs/en/ibm-mq/9.3?topic=codes-json-format-diagnostic-messages

You can filter on a particular field by either:

- expanding a log line, clicking on a value, then clicking the search icon
- using the search bar directly and applying a search for `field:value` for example `ibm_messageId:AMQ9999E`
