---
copyright:
  years: 2023
lastupdated: "2023-11-08"
---

{{site.data.keyword.attribute-definition-list}}

# Service Plans
{: #service_plans}

Learn about the characteristics of {{site.data.keyword.mq_full}} service plans
{: shortdesc}

## Reserved Capacity Plan

The Reserved Capacity plan enables a dedicated environment to be configured for queue manager deployment.

- An instance provides 5 VPC of capacity for deploying queue managers
- It can take several hours to provision before it is available to use
- It is billable regardless of the number of queue manager deployments
- It is only compatible with Reserved Deployment plans

To use the dedicated environment create a Reserved Deployment plan and select the Reserved Capacity to use for deployment.  Multiple deployment plans can be attached to a single capacity plan, in this case the capacity will be shared across the deployment plans.
To increase the size of an existing capacity plan raise a [support ticket](https://cloud.ibm.com/docs/mqcloud?topic=mqcloud-mqoc_report_prob) stating the new required size and the instance ID.  The size of a capacity plan can be increased in increments of 5 VPC.

## Plan Features
{: #plan_features}

|  Feature | Lite | Default | Custom Enterprise | Reserved Deployment |
|----------|------|---------|-------------------|---------------------|
| Multi zone availablity |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| Private networking |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| Deployment API |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| Terraform support |  |  |  | ![Checkmark icon](../images/checkmark-icon.svg) |
| MQ client support | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| IBM MQ Advanced Message Security (AMS) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| IBM MQ REST messaging APIs  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| IBM MQ REST administrative APIs  | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| IBM MQ clustering | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |
| Service-Level Agreement | N/A | 99.9% | 99.9% | 99.99% |
| Billing | Free | PAYG | Subscription via IBM Sales' | PAYG |
| Tenancy | multi | multi | multi | single |
| Message limit | 10,000/month | N/A | N/A | N/A |
{: row-headers}
{: class="comparison-table"}
{: caption="Table comparison. Feature availablity by plan type" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the features. The column headers identify which plan supports the feature. To understand which feature is supported in the table, navigate to the row, and find the column for the plan you are interested in."}


