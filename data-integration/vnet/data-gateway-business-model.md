---
title: Virtual network data gateways capacity consumption 
description: This article provides information about the charges incurred by use of the virtual network data gateway.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Virtual network data gateways capacity consumption
The virtual network data gateway is a network security offering that lets you connect your Azure and other data services to Microsoft Fabric and the Power Platform. You can run Dataflow Gen2, Power BI Semantic Models, Power Platform Dataflows, and Power BI Paginated Reports on top of a virtual network data gateway. The virtual network data gateway ensures no traffic is exposed to a public endpoint. In addition, you can force all traffic to your datasource to go through a gateway, allowing for comprehensive auditing of secure data sources. To learn more and get started, refer to [virtual network data gateways](overview.md).

:::image type="content" source="media\vnet-gateway-architecture-no-swift.png" alt-text="Diagram of the virtual network data gateway architecture.":::

## Understand how and where the virtual network consumes capacity

The virtual network data gateway consumes the capacity of a Power BI Premium or Fabric capacity. The virtual network data gateway is infrastructure that supports many different artifacts, like Dataflows Gen2, semantic models, etc. The gateway consumes capacity for the time that it's up and running. As a consequence, the gateway's capacity consumption is consistent regardless of which artifact uses it.

The virtual network data gateway charge is according to the uptime of the virtual network data gateway; uptime is anytime the virtual network data gateway is on. 

A single virtual network data gateway uses two cores. The CU consumption rate is a fixed rate that we decide, depending on what we want to charge. Learn more about CUs [on the Fabric operations page](/fabric/enterprise/fabric-operations).

Your bill is automatically charged to the capacity linked to your virtual network data gateway. When you signed up for your capacity, you paid for some capacity unit hours. When you use your virtual network, this prepaid amount is consumed. This side of the metrics can only be seen from the consumption metrics app. A single virtual network data gateway uses two cores. The CU consumption rate is a fixed rate. Learn more about CUs [on the Fabric Azure billing page](/fabric/enterprise/azure-billing). You can still use the gateway if your capacity has less than 4 CU, it just requires that the gateways time share the capacity. In other words, the gateways can't run concurrently.

- Consumption Unit (CU) consumption rate per core: 2x
- Consumption: 2x (CU Consumption rate) * 2 cores (per virtual network data gateway) = 4 CUs per hour

## Best Practices

You can set up your virtual network data gateways and connections on the gateway for free. We start to bill when your first query runs or you run a test connection.

To reduce costs, you can actively manage the time to live on your virtual network data gateway in settings. Learn more [here](manage-data-gateways.md#manage-settings).

To check if your virtual network data gateway is on or off, you can use the status icon on the **Manage connections and gateways** page.

## Example Charges on your capacity

The following table summarizes the capacity consumption you can expect from using a single virtual network data gateway for the designated amount of time.

| Time the virtual network is on | Calculation  | Charge on capacity |
|---------------------|---------------------------|--------------------|
| h hours             | 2 * 2 * hours * members        | 4CU*hours               |
| 30 minutes          | 2 * 2 * 0.5 hours * 1 member | 2CU*hours               |
| 1 hour              | 2 * 2 * 1 hour * 1 member    | 4CU*hours               |
| 2 hours             | 2 * 2 * 2 hours * 1 member   | 8CU*hours               |
| 8 hours             | 2 * 2 * 8 hours * 2 members   | 64CU*hours              |
| 24 hours            | 2 * 2 * 24 hours * 1 member  | 96CU*hours              |

This calculation considers all of the following details:

- CU consumption rate
- 2 cores in a virtual network data gateway
- Number of nodes, called gateway members, deployed

Provide the number of gateway members, sometimes called nodes, in your cluster, and the number of hours they're running.

- CU Consumption fixed rate = 2
- Fixed number of cores per virtual network data gateway = 2
- Number of [gateway members](high-availability-load-balancing.md#how-to-create-a-cluster-of-multiple-virtual-network-data-gateways) is the number of nodes deployed in your cluster. You can check this number in the advanced settings of your virtual network data gateway.

Rate at which capacity is consumed = (CU Consumption rate) * (Number of cores per virtual network data gateway) * (Number of hours) * (Number of gateway members)

Rate at which capacity is consumed = 2 CUs * 2 cores * (Number of hours) * (Number of gateway members)

_Rate at which capacity is consumed = 4 per hour * Number of hours * Number of gateway members_

## View and manage your Bill

To view your bill, use the [Fabric Capacity Metrics app](/fabric/enterprise/metrics-app). 

You see three line items:

|Item Kind|Item Name|Operation |Utilization Type |
|-----------|-----------|----------|-----------------|
|Virtual network data gateway|Virtual network data gateway |Virtual network data gateway uptime  |Background |
|Dataset|Global revenue analytics|Virtual network data gateway|Background |
|Dataset|Global revenue analytics|Dataset on-demand refresh|Background |

Description of each line item by Operation name:

- **Virtual network data gateway uptime** The charge from using the virtual network data gateway. This uptime is billed at $0.72/hour and is consistent across all artifacts.
- **(Dataset) Virtual network data gateway** The charge for compute from executing queries on the M Engine. The Virtual network data gateway hosts the M Engine and reports its usage to the semantic model artifact.
- **(Dataset) Dataset on-demand refresh** The charge for compute from using the Analysis Services engine to execute the semantic model.

The charges from the item kind dataset are the same as they would be without using the virtual network data gateway.

The following diagram illustrates how the cost model works. For example, you can see that under semantic models there are two compute engines. The Analysis Services and Power Query Mashup Engine compute costs are each infrastructure items that incur costs over the virtual network Data Gateway. If you use OneLake for storage, you would be billed for that additional cost too.

:::image type="content" source="media\vnet-business-model.png" alt-text="Diagram showing virtual network data gateway meters.":::

## Related content

[Pricing details for services that can use the data gateway](../gateway/related-services-pricing.md)
