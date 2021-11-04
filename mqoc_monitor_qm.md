---

copyright:
  years: 2021
lastupdated: "2021-10-20"

keywords: IBM MQ, MQ on Cloud, MQ, Sysdig, Monitoring

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

# Monitoring a queue manager with Sysdig
{: #monitor_sysdig}

IBM MQ on Cloud generates metrics from queue managers that are displayed in your IBM Cloud Monitoring instances. IBM Cloud Monitoring is operated by Sysdig in partnership with IBM.
{: shortdesc}

## Platform metrics overview

You can configure 1 instance only of the IBM Cloud Monitoring service per region to collect platform metrics.

 - To configure the Sysdig instance, you must turn on the *platform metrics* configuration setting. 
 - If a Sysdig instance in a region is already enabled to collect platform metrics, metrics from Sysdig-enabled services are collected automatically and available for monitoring through this instance. For more information about Sysdig-enabled services, see [Cloud services](/docs/observability-monitoring?topic=observability-monitoring-monitor-sysdig).

**Important:** To monitor platform metrics, check that the IBM Cloud Monitoring instance is provisioned in the same region where the {{site.data.keyword.mq_full}} instance is provisioned.

## Enabling platform metrics from the {{site.data.keyword.mq_full}} dashboard

Complete the following steps to configure platform metrics:

1. Log in to IBM Cloud.
2. Click **View resources**.
3. In the *Services* section, click the {{site.data.keyword.mq_full}} instance that you plan to monitor.
4. Click the overflow menu. Then, select **Add monitoring** to configure platform metrics in the region of your {{site.data.keyword.mq_full}} instance.
    **Note:** If the menu choices include the option **Monitoring**, then your instance is already configured for platform metrics.
5. Provision an instance of the IBM Cloud Monitoring service.

**Note:** After you provision the Sysdig instance, the *Observabvility* page opens. To continue working with {{site.data.keyword.mq_full}}, go back to the {{site.data.keyword.mq_full}} UI.

For more information about how to configure Sysdig instances to receive queue manager metrics, see [Provisioning an instance](/docs/monitoring?topic=monitoring-provision).

## Viewing metrics

**Important:** To monitor {{site.data.keyword.mq_full}} metrics, you must launch the Sysdig web UI instance that is enabled for platform metrics in the region where your {{site.data.keyword.mq_full}} instance is available.

There are different options to launch the Sysdig web UI and monitor metrics:

### Launching Sysdig web UI from the {{site.data.keyword.mq_full}} dashboard

Complete the following steps to launch the Sysdig web UI from the {{site.data.keyword.mq_full}} dashboard:

1. Log in to IBM Cloud.
2. Click **View resources**.
3. In the *Services* section, click the {{site.data.keyword.mq_full}} instance that you plan to monitor.
4. Click the overflow menu. Then, select **Monitoring**.

A new tab in your browser opens and displays the Default dashboard named Queue Managers within the context of your {{site.data.keyword.mq_full}} instance.

### Launching Sysdig web UI from the Observability page

Complete the following steps to launch the Sysdig web UI from the Observability page:

1. [Launch the Sysdig web UI](/docs/Monitoring-with-Sysdig?topic=Sysdig-launch).
2. Select **DASHBOARDS**.
3. In the **Default Dashboards** section, expand **IBM**.
4. Choose the Queue managers dashboard from the list.

Next, change the scope or make a copy of the *Default* dashboard to monitor an {{site.data.keyword.mq_full}} instance.

## Where to look for {{site.data.keyword.mq_full}} metrics
{: #registry_metrics_region}

The [region](/docs/mqcloud?topic=mqcloud-mqoc_qm_locations) in which {{site.data.keyword.mq_full}} metrics are available corresponds to the region of the queue manger that generated the metrics.

The following table shows the location of {{site.data.keyword.mq_full}} metrics.

| Region for your MQ on Cloud instance | Location of {{site.data.keyword.mq_full}} metrics |
|-----------------|-----------------|
| `us-south` | `Dallas (us-south)` |
| `us-east` | `Washington DC (us-east)` |
| `eu-de` | `Frankfurt (eu-de)` |
| `eu-gb` | `London (eu-gb)` |
| `au-syd` | `Sydney (au-syd)` |
{: caption="Table 1. Location of {{site.data.keyword.mq_full}} metrics" caption-side="top"}


## Metrics dictionary for queue managers
{: metrics-for-qms}

| Metric Name |
|-----------|
| [Alter durable subscription count](#ibm_mq_qmgr_durable_subscription_alter_total) | 
| [Commit count](#ibm_mq_qmgr_commit_total) | 
| [Create durable subscription count](#ibm_mq_qmgr_durable_subscription_create_total) | 
| [Create non-durable subscription count](#ibm_mq_qmgr_non_durable_subscription_create_total) | 
| [Delete durable subscription count](#ibm_mq_qmgr_durable_subscription_delete_total) | 
| [Delete non-durable subscription count](#ibm_mq_qmgr_non_durable_subscription_delete_total) | 
| [Expired message count](#ibm_mq_qmgr_expired_message_total) | 
| [Failed MQCB count](#ibm_mq_qmgr_failed_mqcb_total) | 
| [Failed MQCLOSE count](#ibm_mq_qmgr_failed_mqclose_total) | 
| [Failed MQCONN/MQCONNX count](#ibm_mq_qmgr_failed_mqconn_mqconnx_total) | 
| [Failed MQGET count](#ibm_mq_qmgr_failed_mqget_total) | 
| [Failed MQINQ count](#ibm_mq_qmgr_failed_mqinq_total) | 
| [Failed MQOPEN count](#ibm_mq_qmgr_failed_mqopen_total) | 
| [Failed MQPUT count](#ibm_mq_qmgr_failed_mqput_total) | 
| [Failed MQPUT1 count](#ibm_mq_qmgr_failed_mqput1_total) | 
| [Failed MQSET count](#ibm_mq_qmgr_failed_mqset_total) | 
| [Failed MQSUBRQ count](#ibm_mq_qmgr_failed_mqsubrq_total) | 
| [Failed browse count](#ibm_mq_qmgr_failed_browse_total) | 
| [Failed create/alter/resume subscription count](#ibm_mq_qmgr_failed_subscription_create_alter_resume_total) | 
| [Failed topic MQPUT/MQPUT1 count](#ibm_mq_qmgr_failed_topic_mqput_mqput1_total) | 
| [Got non-persistent messages - byte count](#ibm_mq_qmgr_non_persistent_message_destructive_get_total) | 
| [Got persistent messages - byte count](#ibm_mq_qmgr_persistent_message_get_bytes_total) | 
| [Interval total MQPUT/MQPUT1 byte count](#ibm_mq_qmgr_mqput_mqput1_bytes_total) | 
| [Interval total MQPUT/MQPUT1 count](#ibm_mq_qmgr_mqput_mqput1_total) | 
| [Interval total destructive get](#ibm_mq_qmgr_destructive_get_total) | 
| [Interval total destructive get - byte count](#ibm_mq_qmgr_destructive_get_bytes_total) | 
| [Interval total topic bytes put](#ibm_mq_qmgr_topic_put_bytes_total) | 
| [MQCB count](#ibm_mq_qmgr_mqcb_total) | 
| [MQCLOSE count](#ibm_mq_qmgr_mqclose_total) | 
| [MQCONN/MQCONNX count](#ibm_mq_qmgr_mqconn_mqconnx_total) | 
| [MQCTL count](#ibm_mq_qmgr_mqctl_total) | 
| [MQDISC count](#ibm_mq_qmgr_mqdisc_total) | 
| [MQINQ count](#ibm_mq_qmgr_mqinq_total) | 
| [MQOPEN count](#ibm_mq_qmgr_mqopen_total) | 
| [MQSET count](#ibm_mq_qmgr_mqset_total) | 
| [MQSTAT count](#ibm_mq_qmgr_mqstat_total) | 
| [MQSUBRQ count](#ibm_mq_qmgr_mqsubrq_total) | 
| [Non-persistent - topic MQPUT/MQPUT1 count](#ibm_mq_qmgr_non_persistent_topic_mqput_mqput1_total) | 
| [Non-persistent message MQPUT count](#ibm_mq_qmgr_non_persistent_message_mqput_total) | 
| [Non-persistent message MQPUT1 count](#ibm_mq_qmgr_non_persistent_message_mqput1_total) | 
| [Non-persistent message browse - byte count](#ibm_mq_qmgr_non_persistent_message_browse_bytes_total) | 
| [Non-persistent message browse count](#ibm_mq_qmgr_non_persistent_message_browse_total) | 
| [Non-persistent message get - byte count](#ibm_mq_qmgr_non_persistent_message_get_bytes_total) | 
| [Persistent - topic MQPUT/MQPUT1 count](#ibm_mq_qmgr_persistent_topic_mqput_mqput1_total) | 
| [Persistent message MQPUT count](#ibm_mq_qmgr_persistent_message_mqput_total) | 
| [Persistent message MQPUT1 count](#ibm_mq_qmgr_persistent_message_mqput1_total) | 
| [Persistent message browse - byte count](#ibm_mq_qmgr_persistent_message_browse_bytes_total) | 
| [Persistent message browse - count](#ibm_mq_qmgr_persistent_message_browse_total) | 
| [Persistent message destructive get - count](#ibm_mq_qmgr_persistent_message_destructive_get_total) | 
| [Published to subscribers - byte count](#ibm_mq_qmgr_published_to_subscribers_bytes_total) | 
| [Published to subscribers - message count](#ibm_mq_qmgr_published_to_subscribers_message_total) | 
| [Purged queue count](#ibm_mq_qmgr_purged_queue_total) | 
| [Put non-persistent messages - byte count](#ibm_mq_qmgr_non_persistent_message_put_bytes_total) | 
| [Put persistent messages - byte count](#ibm_mq_qmgr_persistent_message_put_bytes_total) | 
| [Queue Manager file system - bytes in use](#ibm_mq_qmgr_queue_manager_file_system_in_use_bytes) | 
| [Queue Manager file system - free space](#ibm_mq_qmgr_queue_manager_file_system_free_space_percentage) | 
| [Resume durable subscription count](#ibm_mq_qmgr_durable_subscription_resume_total) | 
| [Rollback count](#ibm_mq_qmgr_rollback_total) | 
| [Subscription delete failure count](#ibm_mq_qmgr_failed_subscription_delete_total) | 
| [Topic MQPUT/MQPUT1 interval total](#ibm_mq_qmgr_topic_mqput_mqput1_total) | 
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}

### Alter durable subscription count
{: #ibm_mq_qmgr_durable_subscription_alter_total}

Count of alter durable subscriptions for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_durable_subscription_alter_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 2: Alter durable subscription count metric metadata" caption-side="top"}

### Commit count
{: #ibm_mq_qmgr_commit_total}

The total number of commits for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_commit_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 3: Commit count metric metadata" caption-side="top"}

### Create durable subscription count
{: #ibm_mq_qmgr_durable_subscription_create_total}

Count of create durable subscriptions for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_durable_subscription_create_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 4: Create durable subscription count metric metadata" caption-side="top"}

### Create non-durable subscription count
{: #ibm_mq_qmgr_non_durable_subscription_create_total}

Total non-durable subscription create count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_durable_subscription_create_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 5: Create non-durable subscription count metric metadata" caption-side="top"}

### Delete durable subscription count
{: #ibm_mq_qmgr_durable_subscription_delete_total}

Count of delete durable subscriptions for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_durable_subscription_delete_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 6: Delete durable subscription count metric metadata" caption-side="top"}

### Delete non-durable subscription count
{: #ibm_mq_qmgr_non_durable_subscription_delete_total}

Total non-durable subscription delete count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_durable_subscription_delete_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 7: Delete non-durable subscription count metric metadata" caption-side="top"}

### Expired message count
{: #ibm_mq_qmgr_expired_message_total}

Total number of expired messages for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_expired_message_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 8: Expired message count metric metadata" caption-side="top"}

### Failed MQCB count
{: #ibm_mq_qmgr_failed_mqcb_total}

Total number of failed MQCB for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqcb_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 9: Failed MQCB count metric metadata" caption-side="top"}

### Failed MQCLOSE count
{: #ibm_mq_qmgr_failed_mqclose_total}

Total number of failed MQCLOSE for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqclose_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 10: Failed MQCLOSE count metric metadata" caption-side="top"}

### Failed MQCONN/MQCONNX count
{: #ibm_mq_qmgr_failed_mqconn_mqconnx_total}

Total number of failed MQCONN/MQCONNX for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqconn_mqconnx_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 11: Failed MQCONN/MQCONNX count metric metadata" caption-side="top"}

### Failed MQGET count
{: #ibm_mq_qmgr_failed_mqget_total}

Total number of failed MQGET for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqget_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 12: Failed MQGET count metric metadata" caption-side="top"}

### Failed MQINQ count
{: #ibm_mq_qmgr_failed_mqinq_total}

Total number of failed MQINQ for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqinq_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 13: Failed MQINQ count metric metadata" caption-side="top"}

### Failed MQOPEN count
{: #ibm_mq_qmgr_failed_mqopen_total}

Total number of failed MQOPEN for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqopen_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 14: Failed MQOPEN count metric metadata" caption-side="top"}

### Failed MQPUT count
{: #ibm_mq_qmgr_failed_mqput_total}

Total number of failed MQPUT for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqput_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 15: Failed MQPUT count metric metadata" caption-side="top"}

### Failed MQPUT1 count
{: #ibm_mq_qmgr_failed_mqput1_total}

Total number of failed MQPUT1 for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 16: Failed MQPUT1 count metric metadata" caption-side="top"}

### Failed MQSET count
{: #ibm_mq_qmgr_failed_mqset_total}

Total number of failed MQSET for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqset_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 17: Failed MQSET count metric metadata" caption-side="top"}

### Failed MQSUBRQ count
{: #ibm_mq_qmgr_failed_mqsubrq_total}

Total number of failed MQSUBRQ for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_mqsubrq_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 18: Failed MQSUBRQ count metric metadata" caption-side="top"}

### Failed browse count
{: #ibm_mq_qmgr_failed_browse_total}

Total number of failed browses for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_browse_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 19: Failed browse count metric metadata" caption-side="top"}

### Failed create/alter/resume subscription count
{: #ibm_mq_qmgr_failed_subscription_create_alter_resume_total}

Total number of failed create/alter/resume subscriptions for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_subscription_create_alter_resume_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 20: Failed create/alter/resume subscription count metric metadata" caption-side="top"}

### Failed topic MQPUT/MQPUT1 count
{: #ibm_mq_qmgr_failed_topic_mqput_mqput1_total}

Total number of failed topic MQPUT/MQPUT1 for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_topic_mqput_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 21: Failed topic MQPUT/MQPUT1 count metric metadata" caption-side="top"}

### Got non-persistent messages - byte count
{: #ibm_mq_qmgr_non_persistent_message_destructive_get_total}

Total non-persistent message get count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_destructive_get_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 22: Got non-persistent messages - byte count metric metadata" caption-side="top"}

### Got persistent messages - byte count
{: #ibm_mq_qmgr_persistent_message_get_bytes_total}

Total persistent messages get byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_get_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 23: Got persistent messages - byte count metric metadata" caption-side="top"}

### Interval total MQPUT/MQPUT1 byte count
{: #ibm_mq_qmgr_mqput_mqput1_bytes_total}

Total MQPUT/MQPUT1 byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqput_mqput1_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 24: Interval total MQPUT/MQPUT1 byte count metric metadata" caption-side="top"}

### Interval total MQPUT/MQPUT1 count
{: #ibm_mq_qmgr_mqput_mqput1_total}

Total MQPUT/MQPUT1 count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqput_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 25: Interval total MQPUT/MQPUT1 count metric metadata" caption-side="top"}

### Interval total destructive get
{: #ibm_mq_qmgr_destructive_get_total}

Total number of call to destructive GET for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_destructive_get_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 26: Interval total destructive get metric metadata" caption-side="top"}

### Interval total destructive get - byte count
{: #ibm_mq_qmgr_destructive_get_bytes_total}

Total number of bytes from destructive GET for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_destructive_get_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 27: Interval total destructive get - byte count metric metadata" caption-side="top"}

### Interval total topic bytes put
{: #ibm_mq_qmgr_topic_put_bytes_total}

Total topic bytes put interval for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_topic_put_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 28: Interval total topic bytes put metric metadata" caption-side="top"}

### MQCB count
{: #ibm_mq_qmgr_mqcb_total}

Total MQCB count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqcb_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 29: MQCB count metric metadata" caption-side="top"}

### MQCLOSE count
{: #ibm_mq_qmgr_mqclose_total}

Total MQCLOSE count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqclose_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 30: MQCLOSE count metric metadata" caption-side="top"}

### MQCONN/MQCONNX count
{: #ibm_mq_qmgr_mqconn_mqconnx_total}

Total MQCONN/MQCONNX count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqconn_mqconnx_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 31: MQCONN/MQCONNX count metric metadata" caption-side="top"}

### MQCTL count
{: #ibm_mq_qmgr_mqctl_total}

Total MQCTL count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqctl_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 32: MQCTL count metric metadata" caption-side="top"}

### MQDISC count
{: #ibm_mq_qmgr_mqdisc_total}

Total MQDISC count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqdisc_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 33: MQDISC count metric metadata" caption-side="top"}

### MQINQ count
{: #ibm_mq_qmgr_mqinq_total}

Total MQINQ count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqinq_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 34: MQINQ count metric metadata" caption-side="top"}

### MQOPEN count
{: #ibm_mq_qmgr_mqopen_total}

Total MQOPEN count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqopen_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 35: MQOPEN count metric metadata" caption-side="top"}

### MQSET count
{: #ibm_mq_qmgr_mqset_total}

Total MQSET count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqset_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 36: MQSET count metric metadata" caption-side="top"}

### MQSTAT count
{: #ibm_mq_qmgr_mqstat_total}

Total MQSTAT count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqstat_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 37: MQSTAT count metric metadata" caption-side="top"}

### MQSUBRQ count
{: #ibm_mq_qmgr_mqsubrq_total}

Total MQSUBRQ count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_mqsubrq_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 38: MQSUBRQ count metric metadata" caption-side="top"}

### Non-persistent - topic MQPUT/MQPUT1 count
{: #ibm_mq_qmgr_non_persistent_topic_mqput_mqput1_total}

Total non-persistent topic MQPUT/MQPUT1 count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_topic_mqput_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 39: Non-persistent - topic MQPUT/MQPUT1 count metric metadata" caption-side="top"}

### Non-persistent message MQPUT count
{: #ibm_mq_qmgr_non_persistent_message_mqput_total}

Total non-persistent message MQPUT count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_mqput_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 40: Non-persistent message MQPUT count metric metadata" caption-side="top"}

### Non-persistent message MQPUT1 count
{: #ibm_mq_qmgr_non_persistent_message_mqput1_total}

Total non-persistent message MQPUT1 count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 41: Non-persistent message MQPUT1 count metric metadata" caption-side="top"}

### Non-persistent message browse - byte count
{: #ibm_mq_qmgr_non_persistent_message_browse_bytes_total}

Total non-persistent message browse byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_browse_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 42: Non-persistent message browse - byte count metric metadata" caption-side="top"}

### Non-persistent message browse count
{: #ibm_mq_qmgr_non_persistent_message_browse_total}

Total non-persistent message browse count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_browse_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 43: Non-persistent message browse count metric metadata" caption-side="top"}

### Non-persistent message get - byte count
{: #ibm_mq_qmgr_non_persistent_message_get_bytes_total}

Total non-persistent message get byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_get_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 44: Non-persistent message get - byte count metric metadata" caption-side="top"}

### Persistent - topic MQPUT/MQPUT1 count
{: #ibm_mq_qmgr_persistent_topic_mqput_mqput1_total}

Total persistent topic MQPUT/MQPUT1 count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_topic_mqput_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 45: Persistent - topic MQPUT/MQPUT1 count metric metadata" caption-side="top"}

### Persistent message MQPUT count
{: #ibm_mq_qmgr_persistent_message_mqput_total}

Total persistent message MQPUT count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_mqput_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 46: Persistent message MQPUT count metric metadata" caption-side="top"}

### Persistent message MQPUT1 count
{: #ibm_mq_qmgr_persistent_message_mqput1_total}

Total persistent message MQPUT1 count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 47: Persistent message MQPUT1 count metric metadata" caption-side="top"}

### Persistent message browse - byte count
{: #ibm_mq_qmgr_persistent_message_browse_bytes_total}

Total persistent message browse byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_browse_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 48: Persistent message browse - byte count metric metadata" caption-side="top"}

### Persistent message browse - count
{: #ibm_mq_qmgr_persistent_message_browse_total}

Total persistent message browse count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_browse_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 49: Persistent message browse - count metric metadata" caption-side="top"}

### Persistent message destructive get - count
{: #ibm_mq_qmgr_persistent_message_destructive_get_total}

Total persistent message destructive get count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_destructive_get_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 50: Persistent message destructive get - count metric metadata" caption-side="top"}

### Published to subscribers - byte count
{: #ibm_mq_qmgr_published_to_subscribers_bytes_total}

Total published to subscribers byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_published_to_subscribers_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 51: Published to subscribers - byte count metric metadata" caption-side="top"}

### Published to subscribers - message count
{: #ibm_mq_qmgr_published_to_subscribers_message_total}

Total published to subscribers message count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_published_to_subscribers_message_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 52: Published to subscribers - message count metric metadata" caption-side="top"}

### Purged queue count
{: #ibm_mq_qmgr_purged_queue_total}

Total purged queue count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_purged_queue_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 53: Purged queue count metric metadata" caption-side="top"}

### Put non-persistent messages - byte count
{: #ibm_mq_qmgr_non_persistent_message_put_bytes_total}

Total non-persistent messages put byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_non_persistent_message_put_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 54: Put non-persistent messages - byte count metric metadata" caption-side="top"}

### Put persistent messages - byte count
{: #ibm_mq_qmgr_persistent_message_put_bytes_total}

Total persistent messages put byte count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_persistent_message_put_bytes_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 55: Put persistent messages - byte count metric metadata" caption-side="top"}

### Queue Manager file system - bytes in use
{: #ibm_mq_qmgr_queue_manager_file_system_in_use_bytes}

File system bytes in use for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_queue_manager_file_system_in_use_bytes`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 56: Queue Manager file system - bytes in use metric metadata" caption-side="top"}

### Queue Manager file system - free space
{: #ibm_mq_qmgr_queue_manager_file_system_free_space_percentage}

File system free space for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_queue_manager_file_system_free_space_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 57: Queue Manager file system - free space metric metadata" caption-side="top"}

### Resume durable subscription count
{: #ibm_mq_qmgr_durable_subscription_resume_total}

Count of resume durable subscriptions for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_durable_subscription_resume_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 58: Resume durable subscription count metric metadata" caption-side="top"}

### Rollback count
{: #ibm_mq_qmgr_rollback_total}

Rollback count for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_rollback_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 59: Rollback count metric metadata" caption-side="top"}

### Subscription delete failure count
{: #ibm_mq_qmgr_failed_subscription_delete_total}

Total number of failed subscription deletes for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_failed_subscription_delete_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 60: Subscription delete failure count metric metadata" caption-side="top"}

### Topic MQPUT/MQPUT1 interval total
{: #ibm_mq_qmgr_topic_mqput_mqput1_total}

Total topic MQPUT/MQPUT1 interval for a queue manager

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_mq_qmgr_topic_mqput_mqput1_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, The queue manager name` |
{: caption="Table 61: Topic MQPUT/MQPUT1 interval total metric metadata" caption-side="top"}

## Attributes for Segmentation
{: attributes}

### Global Attributes
{: global-attributes}

The following attributes are available for segmenting all of the metrics listed above

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of public, dedicated or local |
| `Location` | `ibm_location` | The location of the monitored resource - this may be a region, data center or global |
| `Resource` | `ibm_resource` | The resource being measured by the service - typically a indentifying name or GUID |
| `Resource Type` | `ibm_resource_type` | The type of the resource being measured by the service |
| `Resource group` | `ibm_resource_group_name` | The resource group where the service instance was created |
| `Scope` | `ibm_scope` | The scope is the account, organization or space GUID associated with this metric |
| `Service name` | `ibm_service_name` | Name of the service generating this metric |

### Additional Attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the reference above.  Please see the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance the metric is associated with |
| `The queue manager name` | `ibm_mq_qmgr_name` | The queue manager name |

