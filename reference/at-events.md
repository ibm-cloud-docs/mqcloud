---

copyright:
  years: 2016, 2023
lastupdated: "2023-05-17"

keywords: IBM MQ, MQ on Cloud, MQ Activity Tracker events

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.mq_full}} service on the Default and Custom plans in {{site.data.keyword.Bluemix}}.
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/activity-tracker?topic=activity-tracker-getting-started){: new_window}.

## List of events
{: #events}



 {{site.data.keyword.mq_full}} service instances on the Default and Custom plans automatically generate events so that you can track activity on your service.

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
{: caption="Table 1. {{site.data.keyword.mq_full}} events" caption-side="top"}

## Where to view the events
{: #ui}

The following table shows the location (region) in {{site.data.keyword.cloud_notm}} where you can monitor MQ on Cloud events:

| MQ on Cloud service instance location  | Activity Tracker service instance location |
|----------------------------------------|--------------------------------------------|
| `Dallas (us-south)`                    | `Dallas (us-south)`                        |
| `Frankfurt (eu-de)`                    | `Frankfurt (eu-de)`                        |
| `London (eu-gb)`                       | `London (eu-gb)`                           |
| `Washington DC (us-east)`              | `Washington DC (us-east)`                  |
