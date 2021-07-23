---

copyright:
  years: 2016, 2020
lastupdated: "2019-06-21"

keywords: IBM MQ, MQ on Cloud, MQ Activity Tracker events

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

<!-- Name your file `at-events.md` and include it in the Reference nav group in your toc file. -->

# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the IBM MQ on Cloud service on the Default and Custom plans in {{site.data.keyword.Bluemix}}.
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started){:new_window}.

<!-- You can create different sections to group events by area. -->

## List of events
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://cloud.ibm.com/docs/services/cloud-activity-tracker/services?topic=cloud-activity-tracker-cf#catalog. -->

 IBM MQ on Cloud service instances on the Default and Custom plans automatically generate events so that you can track activity on your service.

| Action | Description |
|:-------|:------------|
| mqcloud.queue-manager.create | An event is created when you create a queue manager|
| mqcloud.queue-manager.delete | An event is created when you delete a queue manager|
| mqcloud.queue-manager.update | An event is created when you update a queue manager|
| mqcloud.key-store-cert.create | An event is created when you import a certificate into a key store|
| mqcloud.key-store-cert.delete | An event is created when you delete a certificate from a key store|
| mqcloud.key-store-cert.update | An event is created when you update a certificate in a key store|
| mqcloud.trust-store-cert.create | An event is created when you import a certificate into a trust store|
| mqcloud.trust-store-cert.delete | An event is created when you delete a certificate from a trust store|
| mqcloud.trust-store-cert.update | An event is created when you update a certificate in a trust store|
| mqcloud.admin-credentials.create | An event is created when you create administrator credentials|
| mqcloud.admin-credentials.delete | An event is created when you delete administrator credentials|
| mqcloud.admin-credentials.update | An event is created when you update administrator credentials|
| mqcloud.admin-apikey.create | An event is created when you create an API key for an administrator|
| mqcloud.admin-apikey.update | An event is created when you update an API key for an administrator|
| mqcloud.app-credentials.create | An event is created when you create application credentials|
| mqcloud.app-credentials.delete | An event is created when you delete application credentials|
| mqcloud.app-credentials.update | An event is created when you update application credentials|
| mqcloud.app-apikey.update | An event is created when you update an API key for an application|
| mqcloud.cluster.create | An event is created when you create a cluster|
{: caption="Table 1. IBM MQ on Cloud events" caption-side="top"}

## Where to view the events
{: #ui}

The following table shows the location (region) in {{site.data.keyword.cloud_notm}} where you can monitor MQ on Cloud events:

| MQ on Cloud service instance location  | Activity Tracker service instance location |
|----------------------------------------|--------------------------------------------|
| `Dallas (us-south)`                    | `Dallas (us-south)`                        |
| `Frankfurt (eu-de)`                    | `Frankfurt (eu-de)`                        |
| `London (eu-gb)`                       | `London (eu-gb)`                           |
| `Sydney (au-syd)`                      | `Tokyo (jp-tok)`                           |
| `Washington DC (us-east)`              | `Washington DC (us-east)`                  |
