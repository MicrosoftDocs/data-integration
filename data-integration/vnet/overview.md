---
title: What is a virtual network (VNet) data gateway
description: Virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway.
ms.topic: overview
ms.date: 6/27/2025
---

# What is a virtual network (VNet) data gateway?

A virtual network data gateway lets you connect your Azure and other data services to Microsoft Fabric and the Power Platform. The gateway lets you securely communicate with the data source, execute queries, and transmit results back to the service.

You can run Microsoft Fabric Dataflow Gen2, Fabric data pipelines, Fabric Copy Job, Fabric Mirroring, Power BI semantic models, and Power BI paginated reports on top of a virtual network data gateway.

## Why use the VNet data gateway?

The virtual network data gateway:

- Is a powerful network security offering. It can be used with private endpoints for Azure data sources to ensure that no traffic is ever exposed to a public endpoint.
- Supports Private Link scenarios. To learn more, go to [Virtual networks, Private Links, and Power BI](what-is.md#virtual-networks-private-links-and-power-bi).
- Can be used with public endpoints for Azure, other cloud, and on-premises data sources.
- Hardware is fully managed and it can thus be a more cost effective alternative to the on-premises data gateway.
- Can be used to provide comprehensive auditing for all traffic to your datasource.
- Provides compute isolation enhancing security from cross tenant attacks.

:::image type="content" source="media/vnet-overview.png" alt-text="Diagram of the basic VNet functionality from user to data.":::

## Limitations

- Currently, this feature is available only for Fabric Dataflow Gen2, Fabric data pipelines, Fabric Copy Job, Fabric Mirroring, Power BI semantic models, and Power BI paginated reports. Power BI dataflows and datamarts aren't supported.

- VNet data gateway is currently available for P, F, and A4 or higher (A4, A5, A6, and A7) SKUs. For F SKUs, we recommend that you use F8 and above, but all F SKUs work.

- This feature is currently not supported in GCC L2. We do support GCC L4 (Texas and Virginia) and L5 (DoD East). We support air gapped clouds in US Nat East/West and US Sec East/West.

- You can't change the region, subscription, or resource group for the VNet on which the VNet data gateway was created. This scenario isn't currently supported.

- You might see the errors `InvalidConnectionCredentials` or `AccessUnauthorized` when accessing cloud data sources using OAuth2 credentials, even though the credentials were updated recently, for dataflows. When you use OAuth2 credentials, the gateway currently doesn't support refreshing tokens automatically when access tokens expire. Tokens typically expire 1 hour after the refresh starts, but can expire in less than 1 hour, depending on the data source and the tenant policies.

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

- Users are limited to 1,000 data sources maximum on each VNet gateway. [How to avoid reaching this limit](/data-integration/vnet/data-gateway-faqs#what-do-i-need-to-do-if-i-reach-the-maximum-limit-of-1-000-data-sources-per-user--and-how-do-i-avoid-reaching-this-limit-).
