---
title: What is a virtual network (VNet) data gateway (Preview)
description: Virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway.
ms.topic: overview
ms.date: 11/17/2022
---

# What is a virtual network (VNet) data gateway (Preview)?

The virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway. The VNet data gateway securely communicates with the data source, executes queries, and transmits results back to the service.

![VNet overview.](media/vnet-overview.png)

## Limitations

- Currently, this feature is available only for Fabric Dataflow Gen2, Power BI datasets, Power Platform dataflows, and Power BI paginated reports. Power BI dataflows and datamarts are not supported.
- This feature is currently not supported in GCC L2 and Air Gap clouds.

- You can't change the region, subscription, or resource group for the VNet on which the VNet data gateway was created. This scenario isn't currently supported.

- Power BI datasets:

  - A list of supported data services for Power BI datasets is available in [Supported Azure data services](use-data-gateways-sources-power-bi.md#supported-azure-data-services).

- Power Platform dataflows:

  - For Power Platform dataflows, this feature currently doesn't support the ability to write to a privatized data lake or Dataverse.
  - A list of supported data sources for Power Platform dataflows is available in [Supported data sources](data-gateway-power-platform-dataflows.md#supported-data-sources).
  - The physical VNet data gateway is injected into your virtual network and subnet, so it operates in the same region as the virtual network. 
  - The VNet data gateway can be accessed through the application only from the home region of your tenant. There's currently no option to change the VNet data gateway region.
  - VNet data gateways currently support only admin roles and not "Can Use and Can Use+Share" for Power Platform dataflows.

- Power BI paginated reports:
  - VNet gateways support paginated reports.
  - A list of supported data sources for Power BI paginated reports is available in [Supported data sources for Power BI paginated reports](/power-bi/paginated-reports/paginated-reports-data-sources).
