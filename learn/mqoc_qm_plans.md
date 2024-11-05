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

## Lite Plan

A no-charge plan to enable you to get started with the IBM MQ service on cloud today, for free!

The Lite plan has a limit of up to 10,000 messages per month.

## Default Plan

The Default plan is a flexible pay-as-you-go plan that allows you to provision queue managers in a multi-tenant environment in 4 tier sizes and is charged by Virtual Processor Core Hours.

## Custom Enterprise Plan

The Custom Enterprise plan is a pre-paid subscription plan that is available for customers who have already purchased MQ on Cloud from IBM or an authorized business partner.

It allows you to provision queue managers in a multi-tenant environment in 4 tier sizes and is charged by Virtual Processor Core per Month.

Contact your sales representative for more information about this plan.

## Reserved Capacity Plan

This plan is currently only available in select regions, if the plan does not appear in the IBM Cloud Catalog in your selected region, it is not yet available there.

The Reserved Capacity plan enables a single-tenant environment to be configured for queue manager deployment. The plan is purchased using Capacity Units.

- A Capacity Unit provides 5 VPC of capacity for deploying queue managers.
- It can take several hours to provision a new environment before it is available to use.
- An environment is billable regardless of the number of queue manager deployments.
- Reserved Capacity Units are only compatible with Reserved Deployment plans.

To populate a single-tenant tenant environment with queue managers, create a Reserved Deployment plan and select the Reserved Capacity plan to use for queue manager deployment. You will not be able to deploy queue managers with the Reserved Deployment plan without first having a Reserved Capacity environment.

Multiple Reserved Deployment plans can be attached to a single Reserved Capacity plan, in this case the capacity will be shared across the Reserved Deployment plans. To increase the size of an existing Reserved Capacity plan, raise a support ticket stating the new required size and the Reserved Capacity Instance ID. The entitlement of a Reserved Capacity plan is increased by purchasing additional Capacity Units which equates to increments of 5 VPC.

## Reserved Capacity Subscription Plan

This plan is currently only available in select regions, if the plan does not appear in the IBM Cloud Catalog in your selected region, it is not yet available there.

The Reserved Capacity Subscription plan provides the same features of the Reserved Capacity plan.  However, a subscription is purchased through an IBM Sales team and is drawn from when provisioning instances of this plan.

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
| IBM MQ clustering | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) | ![Checkmark icon](../images/checkmark-icon.svg) |  |
| Service-Level Agreement | N/A | 99.9% | 99.9% | 99.99% |
| Billing | Free | PAYG | Subscription via IBM Sales' | PAYG |
| Tenancy | multi | multi | multi | single |
| Message limit | 10,000/month | N/A | N/A | N/A |
{: row-headers}
{: class="comparison-table"}
{: caption="Table comparison. Feature availablity by plan type" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the features. The column headers identify which plan supports the feature. To understand which feature is supported in the table, navigate to the row, and find the column for the plan you are interested in."}
