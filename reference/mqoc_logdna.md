---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-29"

keywords: IBM MQ, MQ on Cloud, MQ, LogDNA, Logs, Logging

---

{{site.data.keyword.attribute-definition-list}}

# LogDNA Logs
{: #logdna_logs}

{{site.data.keyword.mq_full}} generates platform services logs that are displayed in your LogDNA instances.
{: shortdesc}

For information about how to configure LogDNA instances to receive platform services logs, see [Configuring IBM Cloud service logs](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-config_svc_logs).

{{site.data.keyword.mq_full}} generates platform services logs that are displayed in your LogDNA instances for the following specific cases:

- When the queue manager error logs are updated

## Where to look for {{site.data.keyword.la_full_notm}} logs
{: #registry_logs_region}

The [region](/docs/mqcloud?topic=mqcloud-mqoc_qm_locations) in which an MQ on Cloud log entry is available corresponds to the region of the queue manger that generated the log.

The following table shows the location of MQ on Cloud logs.

| Region for your MQ on Cloud instance | Location of {{site.data.keyword.la_full_notm}} logs |
|-----------------                     |-----------------                                    |
| `us-south`                           | `Dallas (us-south)`                                 |
| `us-east`                            | `Washington DC (us-east)`                           |
| `eu-de`                              | `Frankfurt (eu-de)`                                 |
| `eu-gb`                              | `London (eu-gb)`                                    |
| `au-syd`                             | `Sydney (au-syd)`                                   |
{: caption="Table 1. Location of {{site.data.keyword.la_full_notm}} logs" caption-side="top"}
