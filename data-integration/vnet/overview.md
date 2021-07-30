---
title: What is a virtual network (VNet) data gateway (Preview)
description: Virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway.
author: arthiriyer
ms.reviewer: kvivek
ms.prod: on-premises-data-gateway
ms.topic: overview
ms.date: 07/29/2021
ms.author: arthii
ms.custom: intro-internal
---

# What is a virtual network (VNet) data gateway (Preview)? 

The virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway. The VNet data gateway securely communicates with the data source, executes queries, and transmits results back to the service.

![VNet overview.](media/vnet-overview.png)

## Limitations

- Currently, this feature is available only for Power BI datasets and Power Platform dataflows.
- This feature is currently not supported in sovereign clouds.
- Power BI datasets:

  - A list of supported data services for Power BI datasets is available in [Supported Azure data services](use-data-gateways-sources-power-bi.md#supported-azure-data-services).

- Power Platform dataflows:

  - For Power Platform dataflows, this feature currently doesn't support the ability to write to a privatized data lake or Dataverse.
  - A list of supported data sources for Power Platform dataflows is available in [Supported data sources](data-gateway-power-platform-dataflows.md#supported-data-sources).
  - VNet data gateways are created in your tenant’s home region by default and there's currently no option to change the VNet data gateway region. Based on this limitation, VNet data gateways can only be used in Power platform environments in the home region of your tenant.
  - VNet data gateways currently support only admin roles and not "Can Use and Can Use+Share" for Power Platform dataflows.
