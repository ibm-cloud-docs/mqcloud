---
copyright:
  years: 2023
lastupdated: "2023-11-08"
---

{{site.data.keyword.attribute-definition-list}}

# Reserved Deployment Plan
{: #mqoc_reserved_instance_ha}

This section describes the High Availability (HA) provided by the {{site.data.keyword.mq_full}} service and details of disaster recovery.
The information here is a specific to the Reserved Capacity and Reserved Deployment plans.

## High Availability
{: #mqoc_reserved_instance_ha_qm}

{{site.data.keyword.mq_full}} is deployed using a series of components that are built and deployed as containers into an OpenShift cluster that runs in the particular geographical region you have selected. Each paid queue manager that you deploy exists in its own isolated container and has dedicated CPU, RAM and disk allocated for its use.

An OpenShift cluster consists of multiple worker nodes (e.g. virtual machines) across which the deployed containers are distributed and each container has a health-check and liveness-check defined so that OpenShift will automatically cause the container to be moved from one worker to another in the event of certain types of failure.

The {{site.data.keyword.mq_short}} infrastructure is deployed to 3 data centers per region, also referred to as a "Multi Zone region".  This makes the service resilient to individual worker node or data center issues.

The persistent state of a queue manager such as the defined queues, persistent messages that are contained in those queues and channel sequence state of queue manager channels is stored on a persistent volume that exists outside the container, so when a queue manager container is restarted on a different worker node it still has exactly the same persistent state as when it was running on the original worker node.

The approach described above forms the basis for High Availability within {{site.data.keyword.mq_full}} and ensures that queue managers are able to continue running even in the event of the failure of an individual worker in the cluster.

## High Availability of queue managers
{: #mqoc_reserved_instance_ha_architecture}

The {{site.data.keyword.mq_short}} architecture makes use of the MQ Native HA solution.  This provides resilience across the 3 availablity zones by replicating the queue manager container across those zones.  One of the queue manager replicas is active and synchronously forwards data to the 2 non active replicas.  If the active queue manager container becomes unavailable due to underlying infrastructure changes or failures, one of the replicas will take over and connections will automatically be re-routed to the new active queue manager.  This configuration is opaque to the end user of reserved capacity and reserved deployment plans, and increases the availability of the queue manager over a single instance deployment.

See more information on MQ Native HA [here](https://www.ibm.com/docs/en/ibm-mq/latest?topic=configurations-native-ha)

IBM Cloud contractual service level agreement (SLA) for reserved capacity and reserved deployment plans is referenced in Section 3.2 of the [IBM Cloud Service Description](https://www-03.ibm.com/software/sla/sladb.nsf/sla/bm).

### IBM Responsibilities
{: #mqoc_reserved_instance_ha_ibm_resp}

To enable IBM to restore the service following a catastrophic failure a configuration backup of every paid queue manager is taken every hour and saved in an encrypted format in a storage location outside the active data center. The configuration backup includes the admin definitions of the queues, topics and channels that exist within the queue manager as well as TLS certificates that have been applied, but does not include runtime state such as persistent messages or channel sequence state because runtime state in a queue manager changes so frequently that restoring a copy of that data is typically less desirable to an enterprise than starting from a clean state.

Since restoring a queue manager from this configuration backup results in the loss of the runtime state such as persistent messages it is not an action that is taken lightly by IBM and so the IBM Operations team will first work with the infrastructure provider (e.g. IBM or Amazon Web Services) to recover the existing infrastructure. Only once it has been determined that the original infrastructure cannot be recovered in an acceptable timeframe will the recovery process be activated.

### RTO and RPO (recovery time objective and recovery point objective)
{: #mqoc_reserved_instance_ha_rto_rpo}

In the case a catastrophic failure that results in all 3 zones becoming unavailable
- RTO is 24 hours
- RPO is 1 hour

Note there is no support for cross regional disaster recovery so RTO prereqs that the region has been fully recovered
{: attention}

In the case where a single zone becomes unavailable the
- RTO is <10 seconds
- RPO is 0

### Customer Responsibilities
{: #mqoc_reserved_instance_ha_cust_resp}

Since the cold restore of the queue manager does not retain runtime state such as channel sequence state there may be some administrative action that you will need to take to re-integrate the restored queue manager with your other infrastructure, for example by resetting channel sequence numbers so that channels will successfully communicate. 
