---
title: Virtual network data gateways capacity consumption 
description: This article provides information about the charges incurred by use of the virtual network data gateway.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Virtual network data gateways capacity consumption
The virtual network data gateway consumes the capacity of a Power BI Premium or Fabric capacity. The virtual network data gateway is infrastructure that supports many different artifacts, like Dataflows Gen2, semantic models, etc. The gateway consumes capacity for the time that it's up and running. As a consequence, the gateway's capacity consumption is consistent regardless of which artifact uses it.

To learn more and get started using the VNet data gateway, refer to [virtual network data gateways](overview.md).

:::image type="content" source="media\vnet-gateway-architecture-no-swift.png" alt-text="Diagram of the virtual network data gateway architecture.":::

## Understand how and where the virtual network consumes capacity

The virtual network data gateway charge is according to the uptime of the virtual network data gateway; uptime is anytime the virtual network data gateway is on. 

The virtual network data gateway consumes the capacity of a Power BI Premium or Fabric capacity. Capacities are billed by capacity unit hours, or CU hours. To learn more about CUs, visit the [Fabric operations page](/fabric/enterprise/fabric-operations). The VNET data gateway charges with a fixed CU consumption rate of 4CUs per gateway member (a member is a single gateway node in a cluster).

Your bill is automatically charged to the capacity linked to your virtual network data gateway. When you signed up for your capacity, you paid for some capacity unit hours. When you use your virtual network, this prepaid amount is consumed. This side of the metrics can only be seen from the consumption metrics app. You can still use the gateway if your capacity has less than 4 CUs, it just requires that the gateways time share the capacity. In other words, the gateways can't run concurrently.

- Consumption Unit (CU) consumption rate per gateway member: 4 CUs per hour
- Number of [gateway members](high-availability-load-balancing.md#how-to-create-a-cluster-of-multiple-virtual-network-data-gateways) is the number of nodes deployed in your cluster. You can check this number in the advanced settings of your virtual network data gateway.
- To reduce costs, you can actively manage the time to live on your virtual network data gateway in settings. Learn more [here](manage-data-gateways.md#manage-settings).

_Capacity consumption = (CU Consumption rate) * (Uptime in hours) * (Number of gateway members)_

## Best Practices to Manage Cost

- You can set up your virtual network data gateways and connections on the gateway for free. We start to bill when your first query runs or you run a test connection.
- Configure your queries to run concurrently. Each gateway member can run six queries concurrently.
- Maintain a minimum number of gateway members for your needs. The number of [gateway members](high-availability-load-balancing.md#how-to-create-a-cluster-of-multiple-virtual-network-data-gateways) is the number of nodes deployed in your cluster. You can check and configure this number in the advanced settings of your virtual network data gateway.
- To reduce costs, you can actively manage the time to live on your virtual network data gateway in settings. Learn more [here](manage-data-gateways.md#manage-settings).

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
