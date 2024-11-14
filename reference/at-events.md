---

copyright:
  years: 2016, 2024
lastupdated: "2024-11-14"

keywords: IBM MQ, MQ on Cloud, MQ Activity Tracker events, Activity Tracker, Activity Tracker Router

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.mq_full}}
{: #at_events}



{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.mq_full}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where activity tracking events are generated
{: #at-locations}



## Locations where activity tracking events are sent to {{site.data.keyword.at_full_notm}} hosted event search
{: #at-legacy-locations}



{{site.data.keyword.mq_full}} sends activity tracking events to {{site.data.keyword.at_full_notm}} hosted event search in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1}
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}
{: tab-title="Europe"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}



{{site.data.keyword.mq_full}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green}| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}


## Viewing activity tracking events for {{site.data.keyword.mq_full}}
{: #at-viewing}



You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)


## List of platform events
{: #at_actions_platform}



The following table lists the activity tracking event actions that the {{site.data.keyword.cloud_notm}} platform generates {{site.data.keyword.mq_full}} instances are processed.


| Action                                   | Description |
|------------------------------------------|---------|
| `mqcloud.instance.create`           | An event is generated when you provision a service instance. |
| `mqcloud.instance.update`           | An event is generated when you rename a service instance or when you change the service plan. |
| `mqcloud.instance.delete`           | An event is generated when a service instance is deleted. |
{: caption="Actions that generate platform events" caption-side="bottom"}

## List of management events
{: #at_actions}



{{site.data.keyword.mq_full}} service instances automatically generate events that allow you to track different actions within the service. 

| Action             | Description      |
|--------------------|------------------|
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
{: caption="Actions that generate management events" caption-side="bottom"}
