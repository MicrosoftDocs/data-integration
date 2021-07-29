---
title: What is a virtual network (VNet) data gateway (Preview)
description: virtual network (VNet) data gateway helps you to connect from Microsoft Cloud services to your Azure data services within a VNet without the need of an on-premises data gateway.
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

- Currently, this feature is available only for Power BI datasets
- List of supported data services is available here: [Supported Azure data services](use-data-gateways-sources-power-bi.md#supported-azure-data-services)
- Due to an AAD limitation you may see failures when the following settings are enabled together:
  - Service Endpoint for AAD is enabled on the delegated VNET
  - Conditional Access Policies are enabled for the tenant

  To overcome this AAD limitation, you can try either of the following workarounds:
  - Disable Service Endpoint for AAD and open firewall to allow traffic to AAD (already done)
  - Disable Conditional Access Policy for their Tenant
