---
title: What is a virtual network (VNet) data gateway
description: Virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway.
ms.topic: overview
ms.date: 05/06/2024
---

# What is a virtual network (VNet) data gateway?

The virtual network data gateway lets you connect your Azure and other data services to Microsoft Fabric and the Power Platform to securely communicate with the data source, execute queries, and transmit results back to the service. You can run Dataflow Gen2, Power BI Semantic Models, Power Platform Dataflows, and Power BI Paginated Reports on top of a virtual network data gateway. The virtual network data gateway is a powerful network security offering as it can be used in conjunction with private endpoints for Azure data sources to ensure that no traffic is ever exposed to a public endpoint. In addition, it can be used with public endpoints for Azure, other cloud, and on-premises data sources to connect to data without the need to manage any hardware or use an on-premises data gateway. Another common use is to channel all traffic to your datasource through a gateway to allow for comprehensive auditing of secure data sources.

:::image type="content" source="media/vnet-overview.png" alt-text="VNet overview.":::

## Limitations

- Currently, this feature is available only for Fabric Dataflow Gen2, Power BI semantic models, Power Platform dataflows, and Power BI paginated reports. Power BI dataflows and datamarts are not supported.

- VNet data gateway is currently available for P, F, and A4 or above (A4, A5, A6, and A7) SKUs. For F SKUs we recommend that you use F8 and above but all F SKUs will work.

- This feature is currently not supported in GCC L2. We do support GCC L4 (Texas and Virginia) and L5 (DoD East). We support air gapped clouds in US Nat East/West and US Sec East/West.

- You can't change the region, subscription, or resource group for the VNet on which the VNet data gateway was created. This scenario isn't currently supported.

- You may see the errors "InvalidConnectionCredentials" or "AccessUnauthorized" when accessing cloud data sources using OAuth2 credentials, even though the credentials have been updated recently, for dataflows. When using OAuth2 credentials, the gateway currently doesn't support refreshing tokens automatically when access tokens expire. Tokens typically expire 1 hour after the refresh starts, but can expire in less than 1 hour, depending on the data source and the tenant policies.

- Power BI semantic models:

  - A list of supported data services for Power BI semantic models is available in [Supported Azure data services](use-data-gateways-sources-power-bi.md#supported-azure-data-services).

- Power Platform dataflows:

  - For Power Platform dataflows, this feature currently doesn't support the ability to write to a privatized data lake or Dataverse.
  - A list of supported data sources for Power Platform dataflows is available in [Supported data sources](data-gateway-power-platform-dataflows.md#supported-data-sources).
  - The physical VNet data gateway is injected into your virtual network and subnet, so it operates in the same region as the virtual network. 
  - The VNet data gateway can be accessed through the application only from the home region of your tenant. There's currently no option to change the VNet data gateway region.
  - VNet data gateways currently support only admin roles and not "Can Use and Can Use+Share" for Power Platform dataflows.

- Power BI paginated reports:
  - VNet gateways support paginated reports.
  - A list of supported data sources for Power BI paginated reports is available in [Supported data sources for Power BI paginated reports](/power-bi/paginated-reports/paginated-reports-data-sources).
