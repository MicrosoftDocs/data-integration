---
title: Virtual network data gateways pricing and billing 
description: This article provides information about the charges incurred by use of the virtual network data gateway.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Virtual network data gateways pricing and billing
The virtual network data gateway is a network security offering that lets you connect your Azure and other data services to Microsoft Fabric and the Power Platform. You can run Dataflow Gen2, Power BI Semantic Models, Power Platform Dataflows, and Power BI Paginated Reports on top of a virtual network data gateway. The virtual network data gateway ensures no traffic is exposed to a public endpoint. In addition, you can force all traffic to your datasource to go through a gateway, allowing for comprehensive auditing of secure data sources. To learn more and get started, refer to [virtual network data gateways](overview.md).

:::image type="content" source="media\vnet-gateway-architecture-no-swift.png" alt-text="Diagram of the virtual network data gateway architecture.":::

## Understand how and where the virtual network is billed

The virtual network data gateway is billed to a Power BI Premium or Fabric capacity. The virtual network data gateway is infrastructure that supports many different artifacts, like Dataflows Gen2, semantic models, etc. The gateway is billed for the time that it's up and running. This means its bill is consistent regardless of which artifact uses it. The artifact is also charged as normal as a separate charge.

The virtual network data gateway charge is according to the uptime of the virtual network data gateway; uptime is anytime the virtual network data gateway is on. 

A single virtual network data gateway uses two cores. The CU consumption rate is a fixed rate that we decide, depending on what we want to charge. Learn more about CUs [on the Fabric operations page](/fabric/enterprise/fabric-operations).

Your bill is automatically charged to the capacity linked to your virtual network data gateway. When you signed up for your capacity, you paid for a certain number of capacity unit hours, or CUh. When you use your virtual network, this prepaid amount is drained. This side of the metrics can only be seen from the consumption metrics app. A single virtual network data gateway uses two cores. The CU consumption rate is a fixed rate. Learn more about CUs [on the Fabric Azure billing page](/fabric/enterprise/azure-billing). You can still use the gateway if your capacity has less than 4 CU, it wlil juts require that the gateways time share the capacity. In other words, the gateways cannot run concurrently. 

- Consumption Unit (CU) consumption rate per core: 2x
- Price: 2x (CU Consumption rate) * 2 cores (per virtual network data gateway) * $0.18 (Pay as You Go price for one CU per hour) = $0.72 per virtual network/hour

## Best Practices

You can set up your virtual network data gateways and connections on the gateway for free. We start to bill when your first query runs or you run a test connection.

To reduce costs, you can actively manage the time to live on your virtual network data gateway in settings. Learn more [here](manage-data-gateways.md#manage-settings).

To check if your virtual network data gateway is on or off, you can use the status icon on the **Manage connections and gateways** page.

## Example Charges on your capacity
The following table summarizes the bill you can expect from using a single virtual network data gateway for the designated amount of time.

:::image type="content" source="https://github.com/MicrosoftDocs/data-integration-pr/assets/107279699/32a68141-f942-44bb-8fc8-238b0898c80c" alt-text="image":::

This calculation considers all of the following details:

- CU consumption rate
- 2 cores in a virtual network data gateway
- Number of nodes or gateway members deployed
- Price of the virtual network data gateway infrastructure at $0.18

To calculate the final price you pay, use the following calculation. Provide the number of gateway members, sometimes called nodes, in your cluster, and the number of hours they're running.

- CU Consumption fixed rate = 2
- Fixed number of cores per virtual network data gateway = 2
- Fixed pay-as-you-go price for one CU per hour = $0.18
- Number of [gateway members](high-availability-load-balancing.md#how-to-create-a-cluster-of-multiple-virtual-network-data-gateways) is the number of nodes deployed in your cluster. You can check this number in the advanced settings of your virtual network data gateway.

Price incurred = (CU Consumption rate) * (Number of cores per virtual network data gateway) * (Pay as You Go price per CU per core per hour) * (Number of hours) * (Number of gateway members)

Price incurred = 2 CUs * 2 cores * $0.18 per CU per core per hour * (Number of hours) * (Number of gateway members)

_Price incurred = $0.72 per hour * Number of hours * Number of gateway members_

The following table includes sample calculations of a few scenarios with different uptimes and number of gateway member nodes. The first scenario in the table shows the minimum possible price incurred for using a virtual network data gateway. This scenario entails keeping the gateway on for 30 minutes and using only one node. In this scenario, the final price incurred is $0.36. The final scenario shows the maximum possible price incurred for using a gateway. This scenario entails keeping the gateway always on for 24 hours, and using the maximum high availability cluster setting of five nodes. In this scenario the final price incurred is $86.40.

|Time the virtual network is on |Number of Nodes| Calculation	|Charge on capacity |
|--------------------|---------------|--------------|-------------------|
|h hours	|n Nodes | 2 cores per virtual network * 2 CUs consumed * 0.18 * h * n	|$0.72 * h * n |
|30 minutes	|1 Node | 0.72 * 0.5 hours * 1	|0.36 |
|1 hour	|1 Node | 0.72 * 1 hour * 1 node	|0.72 |
|1 hour	|2 Nodes | 0.72 * 1 hour * 2 nodes	|1.44 |
|2 hours |2 Nodes | 0.72 * 2 hours * 2 node	|2.88 |
|8 hours |3 Nodes | 0.72 * 8 hours * 3 nodes |17.28 |
|24 hours	|3 Nodes | 0.72 * 24 hours * 3 nodes	|51.84 |
|24 hours	|5 Nodes | 0.72 * 24 hours * 5 nodes	|86.40 |

## View and manage your Bill
To view your bill, use the [Fabric Capacity Metrics app](/fabric/enterprise/metrics-app). 

You see three line items:

|Item Kind	|Item Name	|Operation |Utilization Type |
|-----------|-----------|----------|-----------------|
|Virtual network data gateway	|Virtual network data gateway |Virtual network data gateway uptime  |Background |
|Dataset 	|Global revenue analytics	|Virtual network data gateway	|Background |
|Dataset	|Global revenue analytics	|Dataset on-demand refresh	|Background |

Description of each line item by Operation name:
-	**Virtual network data gateway uptime** The charge from using the virtual network data gateway. This uptime is billed at $0.72/hour and is consistent across all artifacts.
-	**(Dataset) Virtual network data gateway** The charge for compute from executing queries on the M Engine. The Virtual network data gateway hosts the M Engine and reports its usage to the semantic model artifact.
-	**(Dataset) Dataset on-demand refresh** The charge for compute from using the Analysis Services engine to execute the semantic model.

The charges from the item kind dataset are the same as they would be without using the virtual network data gateway.

The following diagram illustrates how the cost model works. For example, you can see that under semantic models there are two compute engines (Analysis Service compute and the Power Query Mashup Engine compute) and one infrastructure item for the virtual network Data Gateway that are all charged for. If you use OneLake for storage, you would be billed for that too.

:::image type="content" source="media\vnet-business-model.png" alt-text="Diagram showing virtual network data gateway meters.":::

## Related content

If you're using a Premium Power BI capacity, you can learn more about how to view and manage your bill [here](/power-bi/enterprise/service-admin-premium-manage#manage-capacity).
