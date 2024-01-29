---
title: Virtual network (VNet) data gateways business model
description: Provides information about the bill incurred by the virtual network (VNet) data gateways.
ms.topic: conceptual
ms.date: 01/26/2024
---

# Virtual network data gateways

The VNET Data Gateway is a network security offering that lets you connect your Azure and other data services to Microsoft Fabric and the Power Platform. You can run Dataflow Gen2, Power BI Semantic Models, Power Platform Dataflows, and Power BI Paginated Reports on top of a VNET Data Gateway to ensure that no traffic is exposed to public endpoint. In addition, you can force all traffic to your datasource to go through a gateway, allowing for comprehensive auditing of secure data sources. To learn more and get started, visit [VNET Data Gateways](overview.md).

![VNet data gateway architecture.](media/VNet-gateway-architecture-no-swift.png)

## Summary

The VNET Data Gateway is billed as an additive premium infrastructure charge, associated to a Premium or Fabric capacity. This means that it has its own meter and incurs a bill that is consistent across and in addition to all artifacts. Total Bill of running an artifact through the VNET Data Gateway = Artifact Charge + VNET Data Gateway Charge
The VNET Data Gateway Charge is proportional to your usage of the VNET Data Gateway; we define usage as uptime, or anytime the VNET Data Gateway is on. A single VNET Data Gateway uses two cores.
- CU consumption rate: 2x
- Price: 2x (CU Consumption rate) * 2 cores (per VNET Data Gateway) * $0.18 (Pay as You Go price for one CU per hour) = $0.72 per VNET/hour

## Fabric Capacity Metrics Application
Remember that VNET Data Gateways don't map to a single workspace or artifact. Rather, each gateway incurs a single charge on the capacity that encompasses the uptime of all the other artifacts and workspaces using it to connect to data sources.
It shows up as its own line item in the Fabric Capacity Metrics app with the artifact and workspace name as _VNET Data Gateway_.
In the following picture, each box represents a different meter. A meter keeps track of the bill incurred for whichever service it maps to. For example, the Power Query Compute box represents a meter that tracks the compute used by the Mashup Engine to execute M queries.

![VNet Data Gateway Meters](media/vnet-business-model.png)
